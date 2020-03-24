---
layout: article
title: A dependable term-expansion mechanism
tags:
  - best practices
  - term-expansion
show_edit_on_github: false
aside: false
---

Logtalk provides a *dependable term-expansion mechanism* that gives the
user full and fine-grained control on *if*, *when*, and *how* expansions
are applied. This is accomplished by introducing the concept of *hook object*
and by allowing expansion rules to be defined and applied without relying
on multifile predicates.

A *hook object* is simply an object implementing the
[`expanding`](https://logtalk.org/docs/expanding_0.html#expanding-0)
built-in protocol that declares `term_expansion/2` and `goal_expansion/2`
predicates. This allows sets of expansion rules to be independently loaded,
used, and combined. As the expansion predicate are not declared as
multifile predicates, loading a hook object have no consequence by itself
on the subsequent loading of source files. So... how do we expand a source
file? The first option is to declare in the source file itself the hook
object that should be used to expand it:

```logtalk
:- set_logtalk_flag(hook, my_hook_object).
```

Note that [`set_logtalk_flag/1`](https://logtalk.org/manuals/refman/directives/set_logtalk_flag_2.html)
directives are local to the entity or source file containing them. The second
option is to use the `hook/1` compiler option of the compilation and
loading built-in predicates:

```text
| ?- logtalk_load(source, [hook(my_hook_object)]).
...
```

The third option is to define a default hook object using the
[`set_logtalk_flag/1`](https://logtalk.org/manuals/refman/predicates/set_logtalk_flag_2.html)
predicate (which, unlike the directive, sets global and thus default flag values):

```text
| ?- set_logtalk_flag(hook, my_hook_object).
...
```

By default, at startup, the `hook` flag is not defined. This means that, by
default, no source file is expanded independently of any loaded hook objects.

Notice that only a single hook object can be set at any given time to
expand a source file? What if we want to apply multiple expansions to a
source file? In this case, you need to explicitly define how multiple hook
objects are combined to define an *expansion workflow*. Different expansion
workflow semantics are possible and required depending on the problem. For
example, the expansions may be independent (that doesn't necessarily mean,
however, that the order the expansion rules are applied can be arbitrary or
that their concurrent use is free of trouble...).
The expansions may also be intended to be used as a well defined *pipeline*
with e.g. the terms resulting from an expansion being passed to the next
expansion. Or we may have a more complex workflow combining independent and
linked expansions. To simplify defining expansion workflows, Logtalk provides
[`hook_flows`](https://logtalk.org/manuals/libraries/hook_flows.html) and
[`hook_objects`](https://logtalk.org/manuals/libraries/hook_objects.html)
libraries with ready to use workflows and hook objects.

Logtalk's term-expansion mechanism may sound overly complex, specially for
users of Prolog systems such as SWI-Prolog or YAP where the `term_expansion/2`
and `goal_expansion/2` predicates are multifile and the common practice is
just to dump the predicate definitions into `user` and wait for magic to happen.
Any loaded library (by the user or the system itself) can contribute to a growing
set of expansions, often without the user noticing. This work until conflicts
arise between expansions. For example, consider the following module that counts
the number of facts for the `a/1` predicate and adds a fact with the count:

```logtalk
:- module(m1, []).

:- dynamic(counter_/1).

:- multifile(user:term_expansion/2).
:- dynamic(user:term_expansion/2).

user:term_expansion(begin_of_file, begin_of_file) :-
    retractall(counter_(_)),
    assertz(counter_(0)).
user:term_expansion(a(X), a(X)) :-
    retract(counter_(Old)),
    New is Old + 1,
    assertz(counter_(New)).
user:term_expansion(end_of_file, [total_a(Total), end_of_file]) :-
    counter_(Total).
```

Assume now a `source.pl` file with the following contents:

```logtalk
a(2). a(3). a(5).
b(7).
```

If we load the `m1` module followed by the source file we get:

```text
?- [m1].
true.

?- [file].
true.

?- total_a(Total).
Total = 3.
```

The expansion works as intended. But then we, or someone else, decide to
define an expansion that counts `b/1` predicate facts:

```logtalk
:- module(m2, []).

:- dynamic(counter_/1).

:- multifile(user:term_expansion/2).
:- dynamic(user:term_expansion/2).

user:term_expansion(begin_of_file, begin_of_file) :-
    retractall(counter_(_)),
    assertz(counter_(0)).
user:term_expansion(b(X), b(X)) :-
    retract(counter_(Old)),
    New is Old + 1,
    assertz(counter_(New)).
user:term_expansion(end_of_file, [total_b(Total), end_of_file]) :-
    counter_(Total).
```

Now we get with both expansions loaded:

```text
?- [m1, m2].
true.

?- [source].
true.

?- total_a(Total).
Total = 3.

?- total_b(Total).
Correct to: "total_a(Total)"? no
ERROR: Unknown procedure: total_b/1
ERROR:   However, there are definitions for:
ERROR:         total_a/1
ERROR: 
ERROR: In:
ERROR:   [10] total_b(_22126)
ERROR:    [9] <user>
   Exception: (10) total_b(_11122) ? abort
% Execution Aborted
```

Ouch! The expansions code look sensible but loading the first module prevents
the expansions defined in the second module from working as intended. Can you
debug the problem and explain why? This is, of course, a toy example. In
practice, expansions are often more complex and can be harder to debug when
conflicts arise. It's instructive to reimplement the above example using
Logtalk:

```logtalk
:- object(o1,
    implements(expanding)).

    :- private(counter_/1).
    :- dynamic(counter_/1).

    term_expansion(begin_of_file, begin_of_file) :-
        retractall(counter_(_)),
        assertz(counter_(0)).
    term_expansion(a(X), a(X)) :-
        retract(counter_(Old)),
        New is Old + 1,
        assertz(counter_(New)).
    term_expansion(end_of_file, [total_a(Total), end_of_file]) :-
        counter_(Total).

:- end_object.
```

```logtalk
:- object(o2,
    implements(expanding)).

    :- private(counter_/1).
    :- dynamic(counter_/1).

    term_expansion(begin_of_file, begin_of_file) :-
        retractall(counter_(_)),
        assertz(counter_(0)).
    term_expansion(b(X), b(X)) :-
        retract(counter_(Old)),
        New is Old + 1,
        assertz(counter_(New)).
    term_expansion(end_of_file, [total_b(Total), end_of_file]) :-
        counter_(Total).

:- end_object.
```

We now get:

```text
?- {hook_flows(loader)}.
...
true.

?- {o1, o2}.
...
true.

?- logtalk_load(source, [hook(hook_pipeline([o1,o2]))]).
...
true.

?- total_a(Total).
Total = 3.

?- total_b(Total).
Total = 1.
```

The [`hook_pipeline/1`](https://logtalk.org/docs/hook_pipeline_1.html)
parametric object takes as parameter a list of hook objects and defines
a pipeline of expansions where the results of an expansion by a hook
object are passed for further expansion by the next hook object. Problem
solved. Could the problem have been avoided in the first place? Note
that expansions, specially when provided by libraries (system or
third-party) are often written independently and by different people.
Thus, solving conflicts often requires the definition of an explicit
expansion workflow instead of relying on the default system workflow.

Does the conflicts only occur with term-expansion? What about goal-expansion?
Assume that we want to replace goals such as `X is X0 + 1` with calls
to the de facto standard `succ/2` predicate:

```logtalk
:- module(succ_expansion, []).

:- multifile(user:goal_expansion/2).
:- dynamic(user:goal_expansion/2).

user:goal_expansion(X is X0 + 1, succ(X0,X)).
```

We may have a second expansion rule in another module that recognizes
ground `X is X0 + 1` goals and replaces them with either `true` or
`fail`:

```logtalk
:- module(is_optimization, []).

:- multifile(user:goal_expansion/2).
:- dynamic(user:goal_expansion/2).

user:goal_expansion(X is X0 + 1, Goal) :-
    ground(X is X0 + 1),
    (X is X0 + 1 -> Goal = true; Goal = fail).
```

If the expansion rule in the `succ_expansion` module is applied first,
the expansion rule in the `is_optimization` module will never be applied.
The reverse order would work. But relying on the order expansions are
applied only works reliable when we have full control of the order by
using an explicit expansion workflow.

Can we emulate in Logtalk the convenience of the term-expansion mechanism
as found in e.g. SWI-Prolog? It's a fair question and the answer is yes.
We can set the default `hook` object to `user` and define multifile
`term_expansion/2` and `goal_expansion/2` predicates disregarding the
`expanding` built-in protocol. It's also possible to use the more structured
Logtalk implementation of term-expansion while defining workflows with
steps that use expansion rules defined in modules (see e.g. the [`prolog_module_hook/1`](https://logtalk.org/docs/prolog_module_hook_1.html)
parametric hook object provided by the `hook_objects` library).

P.S. When comparing with other term-expansion implementations, we implicitly
focused here only on Prolog systems whose term-expansion mechanism is
derived from the original Quintus Prolog mechanism and based on the
definition of `term_expansion/2` and `goal_expansion/2` multifile
predicates. This mechanism is found on SWI-Prolog and YAP as mentioned.
What about other Prolog systems? Similar to the original Quintus Prolog
implementation, XSB only supports the `term_expansion/2` predicate.
SICStus Prolog uses predicates with the same names but with additional
arguments to better handling passing layout information. GNU Prolog only
provides limited support for the `term_expansion/2` predicate. A few
systems, notably Ciao, ECliPSe, and Qu-Prolog provide different support
for expanding terms. As this short overview makes clear, there isn't any
de facto standard Prolog term-expansion mechanism. Moreover, only some
Prolog systems provide a term-expansion mechanism.
