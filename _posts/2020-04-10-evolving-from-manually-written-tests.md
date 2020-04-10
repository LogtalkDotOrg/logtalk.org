---
layout: article
title: Evolving from manually written tests
tags:
  - best practices
  - testing
show_edit_on_github: false
aside: false
---

Testing is one of the corner stones of writing reliable software. There is
also e.g. code inspections and formal methods but that's a topic for another
post. Here, we will focus on *unit testing* with unit meaning an object or a
Prolog module. This is a followup to our
[previous](../../../2019/08/20/easily-quickcheck-your-predicates.html)
introductory post on *property-based testing*.

Manually written tests
----------------------

Tests can (and often are) written manually. A good starting point when testing
an object (or a Prolog module) is its public interface. For example, consider
the [`enumerate/2`](https://logtalk.org/library/randomp_0.html#enumerate-2)
predicate declared in the
[`randomp`](https://logtalk.org/library/randomp_0.html) library protocol:

```logtalk
:- public(enumerate/2).
:- mode(enumerate(+list(term), --term), zero_or_more).
:- info(enumerate/2, [
    comment is 'Enumerates the elements of a list in random order. Fails if the list is empty.',
    argnames is ['List', 'Random']
]).
```

From the predicate mode directive and description and also from typical
predicate calls, we can start writing some tests:

```logtalk
test(random_enumerate_2_empty_list, fail) :-
    enumerate([], _).

test(random_enumerate_2_singleton_list, true(Random == 1)) :-
    enumerate([1], Random).

test(random_enumerate_2_non_singleton_list, true(List == [1,2,3])) :-
    setof(Random, enumerate([1,2,3], Random, List).

test(random_enumerate_2_non_repetitions, true(List == [1,1,1])) :-
    bagof(Random, enumerate([1,1,1], Random, List).
```

This is a valid approach to testing. But can also be a risky one as often
the tests focus on familiar usage patterns of the code being tested. We can
miss some less common cases. We can also miss some corner or unexpected cases.
This is specially true when the tests are written *after* the code being
tested and/or by same person that wrote the code, which can easily introduce
bias.

Consider the following example taken from our
[previous](../../../2019/08/20/easily-quickcheck-your-predicates.html)
post:

```logtalk
every_other([], []). 
every_other([_, X| L], [X | R]) :- 
    every_other(L, R). 
```

The predicate is supposed to construct a list by taking every other element of
an input list. For example:

```text
| ?- every_other([1,2,3,4,5,6], List).
List = [2, 4, 6]
yes
```

Assume that we have written the following couple of tests: 

```logtalk
test(every_other_2_empty_list, true(List == [])) :-
    every_other([], List).

test(every_other_2_non_empty_list, true(List == [2, 4, 6])) :-
    every_other([1,2,3,4,5,6], List).
```

The tests pass and we are happy. But the happiness doesn't last. An angry
co-worker or a customer comes back complaining about bugs that are eventually
narrowed down to the following query failing:

```text
| ?- every_other([1,2,3], List).
no
```

Oops! The predicate definition is buggy. We rush back to out test suite and
notice that we failed to test lists with an odd number of elements! This is,
of course, a simple example. Just a single predicate with a small number of
clauses, even after fixing the bug. A simple code inspection would have
noticed the bug. 

But consider now a less trivial problem. For example, this StackOverflow [question](https://stackoverflow.com/questions/61079223/prolog-deleting-pairs-with-the-same-first-value-from-list/61085791) 
where we have as input a list of `obj/2` terms and we want to output a list
with all the elements that share the same first value removed. For example:

```text
| ?- filter([obj(x,y),obj(x,z),obj(a,b),obj(b,c)], Filtered).
Filtered = [obj(a,b),obj(b,c)
yes
```

Can we solve this problem efficiently? Assuming that the elements of the
list are ground, we can start by noticing that sorting the list will
cluster together all elements that shared the first argument in the
`obj/2` compound term. For example:

```text
| ?- sort([obj(x,y),obj(x,z),obj(a,b),obj(b,c)], S).
S = [obj(a, b), obj(b, c), obj(x, y), obj(x, z)]
yes
```

Note that the `sort/2` is a standard built-in predicate. Any decent Prolog
system should implement it with a worst case complexity of O(n*log(n)).
After sorting, we can walk the list to filter it, which we can do in O(n).
I suggested the following solution:

```logtalk
filter(List, Filtered) :-
    sort(List, Sorted),
    walk(Sorted, Filtered).

walk([], []).
walk([obj(X,Y)| Sorted], Filtered) :-
    walk(Sorted, X, obj(X,Y), Filtered).

walk([], _, Element, [Element]).
walk([obj(X,_)| Sorted], X, _, Filtered) :-
    !,
    delete(Sorted, X, Rest),
    walk(Rest, Filtered).
walk([obj(X,Y)| Sorted], _, Element, [Element| Filtered]) :-
    walk(Sorted, X, obj(X,Y), Filtered).

delete([], _, []).
delete([obj(X,_)| Sorted], X, Rest) :-
    !,
    delete(Sorted, X, Rest).
delete(Rest, _, Rest).
```

We have four predicates: a main predicate, `filter/2`, and three auxiliary
predicates. A bug can lurk somewhere in any of the predicates. Should we test
only the main predicate and assume that the tests will also cover the auxiliary
predicates? Logtalk [`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html)
tool supports code coverage at the
predicate clause level, thus providing an answer to this question. But simply
ensuring that all clauses are triggered by our tests is by itself a weak
guarantee of correcteness. It doesn't tell us if we test e.g. all possible
corner cases for each predicate. But there is an alternative to write a
relatively large set of tests.

Automatically generating tests
------------------------------

We can use *property-based testing* to automatically generate tests. The
idea is that we define *properties* that our code must satisfy and then
*automatically* generate tests that check that property by generating
random arguments to input arguments and type-checking the output arguments.
For the problem at hand, three properties stand out:

- All elements of the output list must be in input list.
- No two elements in the output list should share the first argument.
- All elements in the input list whose first argument is not repeated must be in the output list.

We can implement these properties using the following predicate:

```logtalk
property(List, Filtered) :-
    filter(List, Filtered),
    % all elements of the output list must be in input list
    forall(
        member(X, Filtered),
        member(X, List)
    ),
    % no two elements in the output list should share the first argument
    \+ (
        select(obj(X,_), Filtered, Rest),
        member(obj(X,_), Rest)
    ),
    % all elements in the input list whose first argument is
    % not repeated must be in the output list
    \+ (
        select(obj(X,Y), List, Rest),
        \+ member(obj(X,_), Rest),
        \+ member(obj(X,Y), Filtered)
    ).
```

But there's a catch. Property-based testing requires that we be able to
generate lists with `obj/2` elements. The
[`type`](https://logtalk.org/library/type_0.html) and
[`arbitrary`](https://logtalk.org/library/arbitrary_0.html)
library entities define a large number of types and generators
for random values of most of those types but not for lists of `obj/2`
terms. The solution? We cheat! First we do a syntactic transformation from
`obj(X,Y)` terms to `X-Y` terms as this standard pair representation is
natively supported by the library. This transformation doesn't change the
semantics of the predicates being tested:

```logtalk
filter(List, Filtered) :-
    sort(List, Sorted),
    walk(Sorted, Filtered).

walk([], []).
walk([X-Y| Sorted], Filtered) :-
    walk(Sorted, X, X-Y, Filtered).

walk([], _, Element, [Element]).
walk([X-_| Sorted], X, _, Filtered) :-
    !,
    delete(Sorted, X, Rest),
    walk(Rest, Filtered).
walk([X-Y| Sorted], _, Element, [Element| Filtered]) :-
    walk(Sorted, X, X-Y, Filtered).

delete([], _, []).
delete([X-_| Sorted], X, Rest) :-
    !,
    delete(Sorted, X, Rest).
delete(Rest, _, Rest).
```

We must of course apply the same syntactic transformation to the `property/2`
predicate:

```logtalk
property(List, Filtered) :-
    filter(List, Filtered),
    % all elements of the output list must be in input list
    forall(
        member(X, Filtered),
        member(X, List)
    ),
    % no two elements in the output list should share the first argument
    \+ (
        select(X-_, Filtered, Rest),
        member(X-_, Rest)
    ),
    % all elements in the input list whose first argument is
    % not repeated must be in the output list
    \+ (
        select(X-Y, List, Rest),
        \+ member(X-_, Rest),
        \+ member(X-Y, Filtered)
    ).
```

We can now use a property-based testing implementation such as Logtalk
`lgtunit` tool [QuickCheck](https://logtalk.org/manuals/devtools/lgtunit.html#quickcheck)
implementation:

```text
| ?- lgtunit::quick_check(
         property(+list(pair(char,char)), -list(pair(char,char)))
     ).
% 100 random tests passed
% starting seed: seed(25256,26643,1563)
yes
```

Are we done? Not really. The top-level interpreter is handy for quick
interactive testing but running tests is usually automated using a
continuous integration (CI) server. As `lgtunit` supports QuickCheck
[*test dialects*](https://logtalk.org/manuals/devtools/lgtunit.html#test-dialects),
we can easily move the tests to a source file:

```logtalk
:- object(tests).

    ...

    quick_check(
        filter_2_test,
        property(+list(pair(char,char)), -list(pair(char,char)))
    ).

    ...

:- end_object.
```

Are we there yet? Well... no. QuickCheck tests can fail like any other kind of
tests. When that happens, guided by the counter-example produced by QuickCheck,
we debug the code and eventually fix it. To illustrate, let us go back to the
initial example with the `every_other/2` predicate. A simple test will expose
the bug:

```text
| ?- lgtunit::quick_check(every_other(+list(integer), -list(integer))).
*     quick check test failure (at test 2 after 0 shrinks):
*       every_other([0],A)
*     starting seed: seed(3172,9814,20125)
no
```

Basides the counter-example, `every_other([0],A)`, the warning message
includes the starting seed (which should be regarded as an opaque term)
for the pseudo-random generator that are used by the `arbitrary` category
predicates, called by the `quick_check/1` predicate (the use of a
pseudo-random generator is key for test reproducibility, as we explain next).

We can fix this particular bug by rewriting the predicate:

```logtalk
every_other([], []).
every_other([H| T], L) :-
    every_other(T, H, L).

every_other([], X, [X]).
every_other([_| T], X, [X| L]) :-
    every_other(T, L).
```

By retesting with the same starting seed that uncovered the bug, the same
random test that found the bug will be generated and run again:

```text
| ?- lgtunit::quick_check(
         every_other(+list(integer), -list(integer)),
         [rs(seed(3172,9814,20125))]
     ).
% 100 random tests passed
% starting seed: seed(3172,9814,20125)
yes
```

When automating the tests, we need to keep the ability to pass the random seed
that uncovers a bug to the tests object so that we can re-test. Test automation
typically uses the `logtalk_tester` automation script. This script accepts
passing arbitrary arguments to the Logtalk process. For example:

```bash
$ logtalk_tester -- "seed-seed(3172,9814,20125)"
```

We can anticipate in the tests object the user passing an optional starting
random seed by defining the optional `setup/0` predicate to look into the
command-line arguments if any:

```logtalk
:- object(tests).

    ...

    setup :-
        (   os::command_line_arguments(Arguments),
            list::member(Argument, Arguments),
            read_term_from_atom(Argument, seed-Seed, []) ->
            type::set_seed(_RandomSeed_)
        ;   true
        ).

    ...

:- end_object.
```

There isn't unfortunately a standard predicate that can read a term from an
atom. Above we used the SWI-Prolog proprietary `read_term_from_atom/3`
built-in argument. Some other Prolog systems provide similar predicates. You
will need to consult the documentation of the backend Prolog system that you
use to run Logtalk.

Which testing approach should be used
-------------------------------------

In general, there's no need to choose. We can use both manually written tests
and property-based testing. In some cases, is worth thinking of the manually
written tests as a first line of defense, followed by (more) deep testing using
property-based testing. Tests are also inevitably an operational documentation
of the code expected behavior and semantics. The definition of code properties
is particularly valuable in clarifying and documenting the expected semantics.

**Note:** The starting seed information and options require the current
Logtalk [git version](https://github.com/LogtalkDotOrg/logtalk3) or the
forthcoming 3.38.0 release, expected to be available by end of April,
beginning of May.
