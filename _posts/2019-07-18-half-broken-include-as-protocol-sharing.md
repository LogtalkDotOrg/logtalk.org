---
layout: article
title: "Half-broken hacks: include/1 as protocol sharing"
tags:
  - modules
  - protocols
  - half broken hacks
show_edit_on_github: false
aside: false
---

This is the third post of a serie about half-broken hacks claimed to provide an alternative to Logtalk features. Half-broken means that, although the hack appears to provide a sought after feature on a cursory glance, close examination quickly uncovers limitations, flaws, and corner cases where it fails to provide the desired functionality and semantics.

In the particular case of *protocols* (or *interfaces*), the claim is that they can emulated using the `include/1` directive. As a hack, this is a relative benign one but still with significant limitations. A specification for this directive can be found in the ISO Prolog Core standard:

> 7.4.2.7 `include/1`
> 
> If `F` is an implementation defined ground term designating
> a Prolog text unit, then Prolog text `P1` which contains
> a directive `include(F)` is identical to a Prolog text `P2`
> obtained by replacing the directive `include(F)`in `P1` by
> the Prolog text denoted by `F`.

As the specification makes clear, this directive provides *textual* inclusion of a file in another file (the de facto translation of "text unit"). As an example, assume a `common.pl` file containing the following `export/1` directive:

```logtalk
:- export(sound/0).
```

The `export/1` directive is in turn specified in ISO standard for Prolog modules:

> 6.2.4.2 Module interface directive export/1
> 
> A module interface directive `export(PI)` in the module
> interface of a module `M`, where `PI` is a predicate indicator,
> a predicate indicator sequence or a predicate indicator list,
> specifies that the module `M` makes the procedures designated by
> `PI` available for import into or re-export by other modules.
> 
> A procedure designated by `PI` in a `export(PI)` directive
> shall be that of a procedure defined in the body (or bodies) of
> the module `M`.
>
>No procedure designated by `PI` shall be a control construct, a
>built-in predicate, or an imported procedure.

You likely noticed the word "interface" above in the specification of the directive. Indeed, the ISO standard for Prolog modules also specifies module interfaces. But it does so by only allowing a single implementation for the interface where both share the module name. Given that the essential characteristic of an interface (or protocol) is to allow multiple implementations, no point in wasting time with the useless (and ignored by implementers) concept of interface in the standard. But the `export/1` directive itself is found in some Prolog systems such as ECLiPSe, SWI-Prolog, XSB, and YAP (but not implemented in e.g. SICStus Prolog).

But back to attempting to use the `include/1` directive to share predicate export directives between modules. Using the `common.pl` file, we can define the following modules:

```logtalk
:- module(dog, []).
:- include(common).

sound :-
    write('Woof...'), nl.
```

```logtalk
:- module(cat, []).
:- include(common).

sound :-
    write('Meowww...'), nl.
```

Given that the two modules export the same predicate, we need to load in a way that avoid name clashes. For example, using SWI-Prolog:

```text
?- use_module(dog, []), use_module(cat, []).
true.
```

Consequently, we also need to use explicit-qualified calls to the `sound/0` predicate:

```text
?- dog:sound.
Woof...
true.

?- cat:sound.
Meowww...
true.
```

As illustrated in this simple example, the `include/1` does work as we expected when calling the exported predicate. But a file is not an interface (or protocol). Module and files are not at the same abstraction level. Moreover, given the textual inclusion semantics, and from the perspective of a reflection API, instead of several modules implementing the same interface, we have modules that happen to export the same (subset of) predicates. There's no concept of interface (or protocol) as an entity at the same abstraction level as modules that we can query, document, or assign a version tag. We cannot make a simple query to find which modules implement a given interface. The textual inclusion also results in a small space overhead as the directives are effectively duplicated in each module that includes a file but that's a minor issue.

There is also a more general problem with the implementation of interfaces (or protocols) in a module system that is not related to the `include/1` directive per se but to the lack of a clear distinction between *declaring a predicate* and *defining a predicate* in Prolog. Recall the specification quoted above of the `export/1` directive:

> A procedure designated by `PI` in a `export(PI)` directive
> shall be that of a procedure defined in the body (or bodies) of
> the module `M`.

Let's update the included file, `common.pl`, with a second `export/1` directive:

```logtalk
:- export(sound/0).
:- export(fly/0).
```

Without also updating the `dog` and `cat` modules, the predicate `fly/0` is now declared (that's the essence of an interface of protocol) but not defined. But if we try again to load the modules we now get:

```text
?- use_module(dog, []), use_module(cat, []).
ERROR: Exported procedure dog:fly/0 is not defined
ERROR: Exported procedure cat:fly/0 is not defined
true.
```

I.e. *closed-world assumption* (CWA) semantics doesn't work for predicates that are *declared* but not *defined*. More precisely, CWA doesn't work for declared *static* predicates that are not defined. What about *dynamic* predicates? Let's update the `common.pl` file to:

```logtalk
:- export(sound/0).
:- export(fly/0).
:- dynamic(fly/0).
```

We can now load the `dog` and `cat` modules without errors and get CWA semantics for the `fly/0` dynamic, exported, predicate. For example:

```text
?- dog:fly.
false.
```

Is the lack of CWA semantics for static predicates a significant issue? Predicates are the building block of Prolog 
applications. That includes knowledge representation. Representing e.g. a attribute that can be true or false is orthogonal to that attribute being immutable (static) or changeable (dynamic). Of course, in our example above, we can keep the `fly/0` predicate as exported and static by using the ugly workaround of adding the following clause to any module where calling the predicate should fail:

```logtalk
fly :-
    fail.
```

In contrast, Logtalk provides a [clean design and implementation of protocols](https://logtalk.org/manuals/userman/protocols.html) (interfaces). Protocols are first-class entities (like objects and categories) and can thus be defined, documented, versioned, and queried (using Logtalk reflection API). Logtalk also provides a clear distinction between *declaring a predicate* and *defining a predicate* and [CWA semantics](https://logtalk.org/manuals/glossary.html#term-closed-world-assumption) for all declared predicates, including static predicates.

P.S. For completeness, follows the Logtalk version of the example above. We start by defining the `common` protocol and the `doc` and `cat` objects implementing the protocol:

```logtalk
:- protocol(common).

    :- public([sound/0, fly/0]).

:- end_protocol.
```

```logtalk
:- object(dog, implements(common)).

    sound :-
        write('Woof...'), nl.

:- end_object.
```

```logtalk
:- object(cat, implements(common)).

    sound :-
        write('Meowww...'), nl.

:- end_object.
```

Loading (assuming each entity saved to its own file named after the entity) and sample queries:

```text
?- {common, doc, cat}.
...
true.

?- dog::sound.
Woof...
true.

?- cat::sound.
Meowww...
true.

?- dog::fly.
false.

?- current_protocol(common).
true.

?- protocol_property(common, public(Predicates)).
Predicates = [sound/0, fly/0].
```
