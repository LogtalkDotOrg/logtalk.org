---
layout: article
title: Predicate semantics
tags:
  - semantics
show_edit_on_github: false
aside: false
---

Logtalk inherits but also extends and improves Prolog predicate semantics to provide clear and uniform closed world semantics, support protocols, provide consistent meta-predicate semantics, prevent misusing of multifile predicates, and prevent a number of hacks based on predicate directives that would break encapsulation. This post discusses relevant Prolog predicate semantics, highlighting its issues and limitations, and how they are solved in Logtalk.

### Closed world semantics

Prolog closed world semantics result from its implementation of the *Closed World Assumption* (CWA): what we cannot prove that is true, is assumed to be false. CWA is the logic counterpart of the negation-as-failure implementation in the Prolog inference engine. The materialization of the CWA in Prolog depends on the value of the standard `unknown` flag and on the presence of predicate directives and predicate definitions to distinguish between an *error* and a *failure*.

The `unknown` flag may be set to `error` (its default value), `fail`, or `warning`. In practice, the only sensible value is `error`. A value or `fail` would mask any predicate name typos in the code. A value of `warning` is mainly useful for interactive sessions. Thus, this flag is best regarded as a deprecated legacy flag. It's also a portability hazard as, depending on the Prolog system, the flag may be local to a module (e.g. SWI-Prolog) or global (e.g. SICStus Prolog). In the discussion that follows, we assume that the `unknown` flag is set to `error`.

The ISO Prolog Core standard specifies three predicate directives that are interpreted, besides their intrinsic semantics, as also declaring predicates: `multifile/1`, `dynamic/1`, and `discontiguous/1`. Consider a source file with the following directives:

```
:- discontiguous(foo/1).
:- dynamic(bar/1).
:- multifile(baz/1).
```

Loading this file on e.g. SICStus Prolog, SWI-Prolog, and YAP and calling the declared predicates, results in failures instead of predicate existence errors. In ECLiPSe (running in ISO mode), a call to `foo/1` throws a predicate existence error but calls to `bar/1` and `baz/1` fail as expected. Oddly, the specification that failure is the correct behavior when calling these predicates is found only on the notes on section 7.5 (Database) of the ISO Prolog Core standard:

> NOTES
>
> 1 There is a difference between a procedure which does not
> exist, and one which exists but has no clauses, for example see
> 7.7.7, 8.9.4.
> 
> 2 A procedure may have no clauses if (1) it is specified in a
> directive but no clauses are defined for it, or (2) it is dynamic
> and all clauses have been retracted.

The somehow subtle but important point here is that predicate existence doesn't depend solely on the presence of clauses but also on the presence of directives. Notably, a predicate can be static and have no clauses (this may sound like a fluke but it's actually, as we will discuss next, a significant and essential predicate property).


### Protocols

The distinction between *declaring* a predicate and *defining* a predicate is a direct consequence not only of predicate directives, as discussed above, but also of using modules or objects. In both cases, the programmer defines an interface, i.e. a set of predicate *declarations*, that other modules or objects are expected to use. In the case of modules, we talk about *exported*  predicates. The exact syntax depends on the chosen Prolog systems, however, given the lack of standardization.

Consider the following module definiton, consisting solely of a `module/2` directive:

```logtalk
:- module(foo, [bar/1]).
```

If we try to compile this module using SWI-Prolog, we get a compilation error:

```text
?- [foo].
ERROR: Exported procedure foo:bar/1 is not defined
true.
```

In the case of SICStus Prolog and YAP, compilation itself is successful but trying to call the exported predicate results in a predicate existence error:

```text
| ?- [foo].
% compiling foo.pl...
%  module foo imported into user
% compiled foo.pl in module foo, 6 msec 34576 bytes
yes
| ?- foo:bar(_).
! Existence error in foo:bar/1
! procedure foo:bar/1 does not exist
! goal:  foo:bar(_443)
```

ECLiPSe doesn't use `module/2` directives. The equivalent module definition would be:

```logtalk
:- module(foo).
:- export(bar/1).
```

Trying to compile the module results in a compilation warning. Trying to call the exported predicate results in a predicate existence error as in the previous systems:

```text
[eclipse 17]: [foo].
...
foo.ecl    compiled 0 bytes in 0.00 seconds
WARNING: predicate declared but not defined in bar / 1 in module foo

Yes (0.06s cpu)
[eclipse 18]: foo:bar(_).
calling an undefined procedure foo : bar(_65) in module eclipse
Abort
```

In the above example, the compiler knows that the module `foo` exports the predicate `bar/1` but cannot separate that predicate declaration from the (non-existing) predicate definition and provide us with closed world semantics. In the case of SWI-Prolog, a predicate definition is required at compile time. For the other systems, the `foo:bar/1` goal throws an error instead of failing. The requirement that an exported predicate be defined is also found on the ISO Prolog Modules standard. But this is an odd requirement: Prolog gives us closed world semantics for `multifile/1`, `dynamic/1`, and `discontiguous/1` directives but not for `export/1` or `module/2` directives!

The Logtalk equivalent to the module `foo` above is the object `foo`:

```logtalk
:- object(foo).

    :- public(bar/1).

:- end_object.
```

After loading the source file defining the object, sending a `bar/1` message fails as expected:

```text
| ?- {foo}.
...
yes

| ?- foo::bar.
no
```

Logtalk materialization of the closed world semantics is clear and uniform. Sending a message corresponding to a declared but not defined predicate, or calling a declared predicate with no clauses, fails. Messages or calls to undeclared predicates generate an error. Having closed world semantics for all declared predicates is fundamental for the definition of *protocols*. A Logtalk protocol is a first-class entity that contains predicate directives, i.e. predicate *declarations*. These *declared* predicates, however, may or may not be *defined* by any object declaring that it implements the protocol. A simple example:

```logtalk
:- protocol(mobility).

    :- public([
        runs/0, flies/0, swims/0
    ]).

:- end_protocol.


:- object(hummingbird, implements(mobility)).

    flies.

:- end_object.


:- object(penguin, implements(mobility)).

    runs.
    swims.

:- end_object.
```

We can send to any object implementing the `mobility` protocol the messages `runs/0`, `flies/0`, and `swims/0`. For example:

```text
| ?- penguin::flies.
no
```

### Consistent meta-predicates semantics

Prolog modules support explicitly-qualified predicate calls, using the `:/2` control construct, and implicitly-qualified predicate calls, using `use_module/1-2` directives. Prolog modules systems are strongly biased towards implicit qualification. But using implicit or explicit qualification, a feature common to many programming languages, is expected to be a first and foremost a matter of programming style and programmer preference. Prolog modules, however, provide different semantics for implicit and explicit qualified calls to meta-predicates. Calling a module meta-predicate using implicit qualification results in the meta-arguments being called in the meta-predicate *calling context*. But calling the same module meta-predicate using explicit qualification results in the meta-arguments being called in the meta-predicate *definition context*, not in the calling context. A simple example, assuming a library module `apply` exporting a `maplist/3` meta-predicate:

```logtalk
:- module(test, [implicit/1, explicit/1]).

:- use_module(library(apply), [maplist/3]).

implicit(Words) :-
    maplist(foo, [1,2,3], Words).

explicit(Words) :-
    apply:maplist(foo, [1,2,3], Words).

foo(1, one).
foo(2, two).
foo(3, three).
```

Trying both `implicit/1` and `explicit/1` predicates:

```text
| ?- use_module(test).
yes

| ?- implicit(Words).
Words = [one, two, three]
yes

| ?- explicit(Words).
ERROR: error(existence_error(procedure,apply:foo/2), ...)
```

The exact details of how an error is reported depends on the Prolog system. But the existence error arguments make it clear that, by explicitly-qualifying the call to the `maplist/3` meta-predicate, the lookup module for the goal constructed from the closure argument is the meta-predicate definition context, `apply`, not the meta-predicate calling context, `test`. The ugly workaround is to explicitly-qualify all the meta-arguments using the calling context:

```logtalk
explicit(Words) :-
    apply:maplist(test:foo, [1,2,3], Words).
```

In Logtalk, implicit message sending, using `uses/2` directive to resolve the messages, and explicit message sending, using the `::/2` control construct, have the same semantics for both meta-predicates and non meta-predicates. I.e. using using implicit or explicit messages is simply a matter of coding style. For meta-predicates, this results in clear and clean meta-predicate call semantics: meta-arguments are always called in the meta-predicate calling context. The Logtalk version of the example above is:

```logtalk
:- object(test).

    :- public([
        implicit/1, explicit/1
    ]).

    :- uses(meta, [map/3]).

    implicit(Words) :-
        map(foo, [1,2,3], Words).

    explicit(Words) :-
        meta::map(foo, [1,2,3], Words).

    foo(1, one).
    foo(2, two).
    foo(3, three).

:- end_object.
```

Both `implicit/1` and `explicit/1` predicate calls give the same results as expected:

```text
| ?- {meta(loader), test}.
yes

| ?- test::implicit(Words).
Words = [one, two, three]
yes

| ?- test::explicit(Words).
Words = [one, two, three]
yes
```

### Multifile predicates

Originally, a multifile predicate was simply a predicate whose clauses could be spread in several files. Nowadays, in the presence of module or object systems, a multifile predicate is associated with a given module or object. The module or object that virtually contains all the predicate clauses is said to contain the multifile predicate *primary declaration*. A simple example using modules:

```logtalk
:- module(main, [foo/1]).

:- multifile(foo/1).
foo(main).
```

```logtalk
:- module(more, []).

:- multifile(main:foo/1).
main:foo(more).
```

```logtalk
:- module(other, []).

:- multifile(main:foo/1).
main:foo(other).
```

The module `main` holds the primary declaration of the `foo/1` multifile predicate. The other two modules, `more` and `other`, contribute clauses for the `main:foo/1` predicate:

```text
| ?- main:foo(X).
X = main ;
X = more ;
X = other ;
no
```

This example, rewritten using Logtalk objects, gives the same results. But the compiler requires a primary declaration before accepting objects (or categories) contributing clauses for the multifile predicate. In the Logtalk version of the above example, the object `main` must be compiled prior to the compilation of the objects `more` and `other`. You may ask: Why does it matter? Why worry with loading order? Consider the following modules:

```logtalk
:- module(hack, []).

:- multifile(trustworthy:foo/0).
trustworthy:foo :-
    write('Nasty business\n'),
    !.
```

```logtalk
:- module(trustworthy, [foo/0]).

foo :-
    write('Well behaved\n').
```

If you load these two modules in e.g. SWI-Prolog or YAP and call the predicate `foo/0`, you will get:

```text
?- [hack, trustworthy].
true.

?- foo.
Nasty business
true.
```

SICStus Prolog, on the other hand, gives:

```text
| ?- [hack, trustworthy].
...
yes

| ?- foo.
Well behaved
yes
```

Trying to compile the ECLiPSe version of the modules results in a compilation error preventing our hack from working. Thus, not an universal problem with module systems (although, in a strict reading, we just exposed yet another Prolog portability gotcha). The behavior of Prolog module systems such as the ones found in SWI-Prolog or YAP is partially a consequence of modules being first and foremost a predicate-prefixing mechanism, not an encapsulation solution. But allowing these hacks not only breaks encapsulation but also means that a client of a module cannot be sure that the module predicate properties (and thus the module interface) are not being changed elsewhere. It should be noted that Prolog module systems like SWI-Prolog or YAP also allow other, similar, nasty tricks such as:

```logtalk
:- module(hack, []).

:- dynamic(trustworthy:foo/0).
```

In this case, we can do:

```text
?- [hack, trustworthy].
true.

?- retractall(foo).
true.

?- foo.
false.
```

Logtalk prevents these and other hacks that take advantage of permissive module systems. For a multifile predicate, a primary declaration, together with a scope directive for the predicate, is required upfront. By not being based on a predicate prefixing mechanism, hacks such as the one above where we covertly make a predicate dynamic are also prevented. Meta-predicate definitions are also verified at compile time to check for [hacks](http://dx.doi.org/10.1007/978-3-540-92995-6_19) playing with meta-predicate templates that would allow breaking encapsulation.
