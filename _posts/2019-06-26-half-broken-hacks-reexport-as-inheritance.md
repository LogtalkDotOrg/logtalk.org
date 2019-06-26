---
layout: article
title: "Half-broken hacks: reexport/1 as inheritance"
tags:
  - modules
  - reexport
  - inheritance
show_edit_on_github: false
aside: false
---

This is the first post of a serie about half-broken hacks claimed to
provide an alternative to Logtalk features. Half-broken means that,
although the hack appears to provide a sought after feature on a
cursory glance, close examination quickly uncovers limitations, flaws,
and corner cases where it fails to provide the desired functionality
and semantics.

In the particular case of the `reexport/1` directive, the claim is that
it provides an implementation of inheritance. A specification for this
directive can be found in the ISO standard for Prolog modules:

> 6.2.4.4 Module interface directive reexport/1
> 
> A module interface directive `reexport(PI)` in the module
> interface of a module `M`, where `PI` is an atom, a sequence of
> atoms, or a list of atoms specifies that the module `M` imports
> all the user defined procedures exported or re-exported by the
> modules designated by `PI` and that `M` makes these procedures
> available for import into or re-exportation by other modules.

Although this standard is basically ignored (for good reasons) by implementers,
the directive itself is found in some Prolog module systems such as Ciao, ECLiPSe,
SWI-Prolog and YAP. It's absent, however, from systems such as SICStus Prolog
and XSB.

As a simple example of an attempt to use the `reexport/1` directive as an
implementation of inheritance, consider the following three modules, each
defined in a source file named after the module:

```logtalk
:- module(m1, [d/1, s/1]).

:- dynamic(d/1).
d(m1).

s(m1).
```

```logtalk
:- module(m2, []).

:- reexport(m1).

s(m2).
```

```logtalk
:- module(m3, []).

:- reexport(m2).
```

The first issue we find is in loading the source files. Due to the predicate
import/export semantics, simply consulting the files either results in an
error (e.g. SWI-Prolog) or in the redefinition of imported predicates in
`user` space (e.g. YAP). To avoid this issue, we can instead use the
`use_module/2` directive with an empty import list. Let's use SWI-Prolog
for the sample queries.

```
?- use_module(m1,[]), use_module(m2,[]), use_module(m3,[]).
Warning: m2.pl:6:
Warning:    Local definition of m2:s/1 overrides weak import from m1
true.
```

The warning we get is due to the "inherited" definition for the `s/1`
predicate from module `m1`, which is redefined in the module `m2`. As
the module `m3` simply reexports the module `m2`, which in turn reexports
module `m1` (claimed to form an "inheritance" chain), let's query it:

```
?- m3:s(X).
X = m2.

?- m3:d(X).
X = m1.
```

So far, so good. We inherit the defintion of `s/1` from `m2` (which
overrides the definition inherited from `m1`) and the defintion of
`d/1` from `m1`. Let's now try to override the definition of `d/1`
in `m2`:

```
?- m2:assertz(d(m2)).
true.

?- m3:d(X).
X = m1 ;
X = m2.
```

We get a different behaviour for the `d/1` dynamic predicate compared
with the `s/1` static predicate. Worse, the first solution we get for
`d/1` is not from the module close to `m3` in the "inheritance" chain,
which is `m2`, but from the `m1`. Not what we expect from a proper
implementation of inheritance. Let's undo the change by retracting all
clauses for `d/1` in the module `m2`:

```
?- m2:retractall(d(_)).
true.
```

Retrying the `m3:d/1` query:

```
?- m3:d(X).
false.
```

Oops! we now lost both the defintion from `m2`, as expected, but also
the definition from `m1`! Let's query `m1` to try to understand what's
happening:

```
?- m1:d(X).
false.
```

The `d1` definition is also gone from `m1` although the `retractall/1`
goal was executed in the context of `m2`.

Thus, not only `reexport/1` gives different "inheritance" semantics
for static and dynamic predicates, which is wrong as the *changeable*
property of a predicate is orthogonal to inheritance, but also the
standard database built-in predicates fail to provide the expected
semantics.

A fair question at this point, given the lack of standardization of
Prolog modules, is if we are observing here a behaviour specific to
SWI-Prolog. Let's try the same sequence of queries on YAP:

```
?- use_module(m1,[]), use_module(m2,[]), use_module(m3,[]).
reconsulting m1...
reconsulted m1.pl in module m1, 1 msec 8144 bytes
reconsulting m2...
m2.pl:6: Module m2 redefines imported predicate m1:s/1.
reconsulted m2.pl in module m2, 1 msec 1352 bytes
reconsulting m3...
reconsulted m3.pl in module m3, 0 msec 1472 bytes
true

?- m3:s(X).
X = m2 ? ;
false.

?- m3:d(X).
X = m1 ? ;
false.

?- m2:assertz(d(m2)).
true

?- m3:d(X).
X = m2 ? ;
false.

?- m2:retractall(d(_)).
true ? ;
false.

?- m3:d(X).
false.

?- m1:d(X).
X = m1 ? ;
false.
```

In this case, the redefinition of `d/1` in module `m2` appears to
work but retracting it doesn't returns to the previous state as
`m3:d/1` stops finding the solution inherited from `m1`. Thus, broken
results as well from an inheritance perspective.

Would ECLiPSe do better here? No. Attempting to load the ECLiPSe versions
of the modules above results in a compilation error:

```
Stream :6:
  trying to redefine an existing imported procedure in s / 1
Error(s) occurred while compiling /Users/pmoura/rex/m2.ecl
Aborting execution ...
Abort
```

From the ECLiPSe documentation on the `reexport/1` directive:

> Reexporting is not compatible with a local definition of the same name (because reexport always implies an import as well), it raises error 92.

The documentation suggests a workaround, which results in the following
updated version of the module `m2`:

```logtalk
:- module(m2).

:- reexport m1 except s/1.
:- export s/1.

s(m2).
```

Trying our sequence of queries:

```
[eclipse 7]: ensure_loaded(m1), ensure_loaded(m2), ensure_loaded(m3).
source_processor.eco loaded in 0.00 seconds
hash.eco   loaded in 0.00 seconds
compiler_common.eco loaded in 0.01 seconds
compiler_normalise.eco loaded in 0.00 seconds
compiler_map.eco loaded in 0.00 seconds
compiler_analysis.eco loaded in 0.00 seconds
compiler_peephole.eco loaded in 0.01 seconds
compiler_codegen.eco loaded in 0.01 seconds
compiler_varclass.eco loaded in 0.00 seconds
compiler_indexing.eco loaded in 0.00 seconds
compiler_regassign.eco loaded in 0.00 seconds
asm.eco    loaded in 0.01 seconds
module_options.eco loaded in 0.00 seconds
ecl_compiler.eco loaded in 0.07 seconds
m1.ecl     compiled 40 bytes in 0.00 seconds
m2.ecl     compiled 40 bytes in 0.00 seconds
m3.ecl     compiled 0 bytes in 0.00 seconds

Yes (0.07s cpu)
[eclipse 8]: m3:s(X).

X = m2
Yes (0.00s cpu)
[eclipse 9]: m3:d(X).

X = m1
Yes (0.00s cpu)
[eclipse 10]: assertz(m2:d(m2)).
trying to redefine an existing imported procedure in assertz(m2 : d(m2))
Abort
```

Thus, in the case of ECLiPSe, we cannot override an "inherited" definition
dynamically at runtime.

It's clear from this simple experiment that, although the `reexport/1`
directive may provide an approximation to inheritance semantics in
limited and controlled setups where portability is not a requirement,
it fails to be a general solution. Are the issues exposed above the
result of bugs that could be fixed? A bug is a deviation from a specification
that formalizes correct behaviour. But there's no mention of inheritance or
inheritance semantics in the standard's specification of either the
directive or the database predicates. Moreover, any "fix" will
need to preserve existing semantics for the directive and predicates
when not being used to try to mimic inheritance.

**Concluding, there's a world of difference between a language designed from the
ground up to provide features such as inheritance, as exemplified by Logtalk,
and twisting Prolog constructs to try to provide features that were never
part of their design and specification.**

P.S. For completeness, follows the Logtalk version of the test modules and
the sample queries:

```logtalk
:- object(m1).

    :- public([d/1, s/1]).
    :- dynamic(d/1).
    
    d(m1).
    
    s(m1).

:- end_object.
```

```logtalk
:- object(m2,
    extends(m1)).

    s(m2).

:- end_object.
```

```logtalk
:- object(m3,
    extends(m2)).

:- end_object.
```

Sample queries:

```
?- {m1, m2, m3}.
% [ m1.lgt loaded ]
% (0 warnings)
% [ m2.lgt loaded ]
% (0 warnings)
% [ m3.lgt loaded ]
% (0 warnings)
true.

?- m3::s(X).
X = m2.

?- m3::d(X).
X = m1.

?- m2::assertz(d(m2)).
true.

?- m3::d(X).
X = m2.

?- m2::retractall(d(_)).
true.

?- m3::d(X).
X = m1.

?- m1::d(X).
X = m1.
```

The Logtalk version is, of course, fully portable. You can use any of the
Logtalk supported backend Prolog compilers to run it.
