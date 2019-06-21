---
title: Prolog modules madness II
author: Paulo Moura
layout: article
tags:
  - semantics
  - modules
show_edit_on_github: false
aside: false
---

Try the following experiment in a Prolog compiler with a module system. Define a simple module containing a simple meta-predicate that tests its meta-argument, writing an error message if it's uninstantiated:

```logtalk
:- module(m, [mp/1]).

:- meta_predicate(mp(0)).

mp(Goal) :-
    (    var(Goal) ->
         write(error)
    ;    write(passed)
    ).
```

Compile and load the code above and we're ready for a quick test. This is the result you get with current versions of SICStus Prolog, SWI-Prolog, and YAP:

```text
| ?- m:mp(_).
passed
yes
```

You get this result no matter how you load the module file. You also get this result if you import the module meta-predicate in order to call it without using explicit qualification:

```text
| ?- mp(_).
passed
yes
```

Before looking closely for an explanation why we don't get an `error` message instead of a `passed` message, allow me to show the result you get in Logtalk with the same meta-predicate definition:

```logtalk
:- object(obj).

    :- public(mp/1).
    :- meta_predicate(mp(0)).

    mp(Goal) :-
        (    var(Goal) ->
             write(error)
        ;    write(passed)
        ).

:- end_object.
```

After compiling an loading this object, we get:

```text
| ?- obj::mp(_).
error
yes
```

Back to the module example. Is the standard `var/1` built-in predicate broken? Or maybe `var/1` isn't module-aware? Should we blame the `meta_predicate/1` directive? But we want it in order to be able to call the meta-predicate without qualifying both the call and the meta-arguments(!) when importing the module. At this point, Prolog module pundits are likely loosing their patience and screaming that the solution is to "correct" the meta-predicate definition to:

```logtalk
mp(_:Goal) :-
    (    var(Goal) ->
         write(error)
    ;    write(passed)
    ).
```

With this "corrected" definition you now get:

```text
| ?- m:mp(_).
error
yes
```

Some will go as far as arguing that, because a simple workaround is available, everything is fine. But one of the main goals of the `meta_predicate/1` directive is to avoid using explicit qualification (as we are now doing in the meta-predicate clause head) in the first place. Wouldn't it be more elegant to make `var/1` (and other built-in predicates!) module-aware? That would fit nicely with the common argument that modules are a natural solution for encapsulation Prolog code. And would avoid the trouble of adding not only a `meta_predicate/1` directive but also modifying the meta-predicate definition when moving a meta-predicate to another module. Not to mention that the original, broken module meta-predicate definition is more elegant, straightforward, easier to explain and understand by novice programmers when compared with the "corrected" definition, which requires understanding the lower-level details of Prolog modules compilation.

**Update:** You may wonder what results you get with other Prolog compilers with modules systems. The problem doesn't exist in ECLiPSe as this compiler uses an alternative solution for declaring and defining meta-predicates. The problem also doesn't exist in the beta versions of Ciao 1.13 where our first attempt at defining the meta-predicate is also the correct one, working similar to Logtalk in this respect.
