---
layout: article
title: The cost of defaulty representations
tags:
  - best practices
  - data
show_edit_on_github: false
aside: false
---

Logic programming applications that acquire and process external data are
common. We don't always have a choice on the format of the data during
acquisition. But we can often decide how to represent the data internally.
Our data representation choices can have a significant performance impact.
To illustrate, consider the simple case of counting the number of atoms
and the number of numbers in a list that can contain atoms, numbers,
and other types of terms that are irrelevant. Assuming that the predicate
computing the counts is named `count_atomics/3`, we can start by defining
a simple protocol to declare it:

```logtalk
:- protocol(processing).

    :- public(count_atomics/3).

:- end_protocol.
```

A possible implementation of this protocol can be:

```logtalk
:- object(bad,
    implements(processing)).

    count_atomics(List, Atoms, Numbers) :-
        count_atomics(List, 0, Atoms, 0, Numbers).

    count_atomics([], Atoms, Atoms, Numbers, Numbers).
    count_atomics([Term| Terms], Atoms0, Atoms, Numbers0, Numbers) :-
        count_atomic(Term, Atoms0, Atoms1, Numbers0, Numbers1),
        count_atomics(Terms, Atoms1, Atoms, Numbers1, Numbers).

    count_atomic(Term, Atoms0, Atoms1, Numbers0, Numbers1) :-
        atom(Term),
        !,
        Atoms1 is Atoms0 + 1,
        Numbers1 is Numbers0.
    count_atomic(Term, Atoms0, Atoms1, Numbers0, Numbers1) :-
        number(Term),
        !,
        Atoms1 is Atoms0,
        Numbers1 is Numbers0 + 1.
    count_atomic(_, Atoms1, Atoms1, Numbers1, Numbers1).

:- end_object.
```

Abstracting the code, we have a common pattern. A pattern that I come across
regularly when working on Prolog codebases. The predicate that processes each
list element, `count_atomic/5`, is composed by a clause per element type where
the body starts with a test, followed by a cut, and then the processing code.
The last clause is a *catchall* clause, handling the terms that we don't
care for. The cuts in previous clauses prevent using the catchall clause on
backtracking. The cuts also mean: we found the correct clause, commit to it.
This is called a *defaulty* representation as we cannot distinguish between
the different elements until we test them.

This is a costly pattern, although one that we can't always avoid. Why
is it costly? When calling a `count_atomic/5` goal, it can unify with
the heads of all the predicate clauses. First-argument indexing cannot
help here as the first argument in all clauses is a variable. That means
that a choice-point is created only to be discarded when we commit to the
correct clause. If the number of calls to this predicate is significant in
a normal run of the application, or if this pattern is used repeatedly
elsewhere, the backtracking and the constant creation and discarding of
choice-points can adversely impact performance.

Can we do better? One alternative is to change the representation of the list
elements by *tagging* them. We can, for example, use a `a/1` compound term
wrapper for atoms, a `n/1` wrapper for numbers, and a `o/1` wrapper for any
other type:

```logtalk
:- object(better,
    implements(processing)).

    count_atomics(List, Atoms, Numbers) :-
        count_atomics(List, 0, Atoms, 0, Numbers).

    count_atomics([], Atoms, Atoms, Numbers, Numbers).
    count_atomics([Term| Terms], Atoms0, Atoms, Numbers0, Numbers) :-
        count_atomic(Term, Atoms0, Atoms1, Numbers0, Numbers1),
        count_atomics(Terms, Atoms1, Atoms, Numbers1, Numbers).

    count_atomic(a(_), Atoms0, Atoms1, Numbers0, Numbers1) :-
        Atoms1 is Atoms0 + 1,
        Numbers1 is Numbers0.
    count_atomic(n(_), Atoms0, Atoms1, Numbers0, Numbers1) :-
        Atoms1 is Atoms0,
        Numbers1 is Numbers0 + 1.
    count_atomic(o(_), Atoms1, Atoms1, Numbers1, Numbers1).

:- end_object.
```

This is a much cleaner representation. We no longer have a catchall clause
or cuts. We can distinguish each element using only clause head
unification. The `count_atomic/5` predicate can be nicely indexed by the
compiler/runtime as the first argument in all clauses is a non-variable
term with distinct functors.

We can use Logtalk's
[`ports_profiler`](https://logtalk.org/manuals/devtools/ports_profiler.html)
tool to compare both alternatives when proving the same query. Assuming
that the protocol and the two alternative implementations are saved in an
`application.lgt` file:

```text
?- logtalk_load(ports_profiler(loader)).
...
true.

?- logtalk_load(application, [debug(on), source_data(on)]).
...
true.

?- bad::atomics_count([a,1,_,b,2,_,c,3,_], As, Ns).
As = Ns, Ns = 3.

?- ports_profiler::data.
-------------------------------------------------------------------------
Entity  Predicate          Fact  Rule  Call  Exit *Exit  Fail  Redo Error
-------------------------------------------------------------------------
bad     count_atomic/5        3    15     9     9     0     0     0     0
bad     count_atomics/3       0     1     1     1     0     0     0     0
bad     count_atomics/5       1     9    10    10     0     0     0     0
-------------------------------------------------------------------------
true.

?- ports_profiler::reset.
true.

?- better::count_atomics([a(a),n(1),o(_),a(b),n(2),o(_),a(c),n(3),o(_)], As, Ns).
As = Ns, Ns = 3.

?- ports_profiler::data.
-------------------------------------------------------------------------
Entity  Predicate          Fact  Rule  Call  Exit *Exit  Fail  Redo Error
-------------------------------------------------------------------------
better  count_atomic/5        3     6     9     9     0     0     0     0
better  count_atomics/3       0     1     1     1     0     0     0     0
better  count_atomics/5       1     9    10    10     0     0     0     0
-------------------------------------------------------------------------
true.
```

The `ports_profiler` tool uses the debugging API to collect data on the number
of times each port is crossed when proving a goal. The tool output reflects the
ports found in the
[*extended procedure box model*](https://logtalk.org/manuals/userman/debugging.html#procedure-box-model)
used by Logtalk. The traditional Prolog procedure box
have four ports: *call*, *exit*, *redo*, and *fail*. To this model, Logtalk adds
three ports: *fact* (when a goal unifies with a fact), *rule* (when a
goal unifies with a rule head), and *error* (when a goal throws an exception).
The `ports_profiler` tool splits the *exit* port between deterministic and
non-deterministic ports, respectively, *exit*  and **exit*.

What can we conclude from the profiling data above? First, in neither case
are there any leftover choice-points as we can check in the **exit* column.
The data only differs, as expected, for the alternative definitions of the
`count_atomic/5` predicate. Our list have 9 elements. The definition in the
`better` object shows the minimun number of unifications required for proving
the query: 9. The definition in the `bad` object shows 3 + 15 unifications
between a goal and the clause heads. The 3 fact unifications are for the
catchall clause as we have three `o(_)` elements in the list. The 15
unifications are for the 9 elements, which means that we backtrack close to
two times per element before finding the correct clause. This gets worse
quickly as the number of cases increases (e.g. counting atoms, integers,
floats, and compounds).

We should mention that the wrappers we used to tag the list elements introduce
a memory overhead. In most cases, this overhead is small when compared with
the performance gains by avoiding unnecessary backtracking and repeated
creation and discarding of choice-points (whose internal representation also
results in a memory overhead). As a data point, I helped in the past optimize
two non-trivial applications processing large datasets where replacing
defaulty representations in critical parts resulted in cuts to processing
time close to 40% in typical runs. As always, use a profiler to identify time
critical areas in your application before rewriting any defaulty representations
(from a strictly performance perspective, optimizations outside those areas may
not be worth the changes required, although the code will become much cleaner,
which is also significant). Even better, try your best to avoid defaulty
representations in the first place when developing new applications.

### Resources

I first learned about *defaulty* representations in Richard O'Keefe book
"The Craft of Prolog", which I highly recommend.

The [`ports_profiler`](https://logtalk.org/manuals/devtools/ports_profiler.html)
can provide other significant insights on query execution besides the particular
case illustrated here. See its documentation for details.
