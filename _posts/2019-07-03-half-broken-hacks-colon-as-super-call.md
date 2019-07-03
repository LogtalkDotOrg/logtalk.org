---
layout: article
title: "Half-broken hacks: :/2 as super call"
tags:
  - modules
  - super call
  - inheritance
  - half broken hacks
show_edit_on_github: false
aside: false
---

This is the second post of a serie about half-broken hacks claimed to provide an alternative to Logtalk features. Half-broken means that, although the hack appears to provide a sought after feature on a cursory glance, close examination quickly uncovers limitations, flaws, and corner cases where it fails to provide the desired functionality and semantics.

In the particular case of *super calls*, the claim is that they can simply be replaced by `:/2` calls. A *super call* is typically used to call an inherited predicate definition from a local redefinition of the predicate. In Logtalk, *super calls* use the `^^/1` control construct and operator, which takes as argument the (inherited) predicate being called. For example:

```logtalk
print_banner :-
    % call the inherited definition of the predicate
    ^^print_banner,
    % add another line to the banner
    write('That''s all Folks!'), nl.
```

The local predicate definition can be described as *specializing* the inherited predicate definition.

Other programming languages, e.g. Smalltalk and Java, use instead a `super` keyword. Abstracting the syntax details, a key property is that **the ancestor entity is not explicitly referenced in a *super call***. Consequently, changes to actual ancestor entity that provides the inherited definition don't require any source code changes to any entities making the *super call*. In a proper implementation of this language feature (such as the one found in Logtalk), the compiler and the runtime take care of the inherited predicate definition lookup. This lookup is performed at compile time whenever possible. But it's never the programmer's responsibility.

But trying to hack a *super call* using the explicit-module qualification `:/2` control construct requires an explicit module argument. That means that changes to a predicate that can be (or is expected to be) specialized can force the programmer to look into all calls to the predicate from other modules to check if any `:/2` goal also requires updating. This is fragile, specially when using third-party libraries.

It's also important to note that the changes may also happen at runtime when working with dynamic predicates. For example, a predicate definition may be asserted in an entity between the entity originally providing the inherited definition and the entity making the *super call* in the ancestor chain. This would immediately break any `:/2` calls used as an hack for *super calls*.

Another key property is that ***super calls* preserve *self***. For example, assume the following default predicate definition, using Logtalk `::/1` message to *self* control construct:

```logtalk
salutation :-
    ::name(Name),
    write('Hello '), write(Name), write('!'), nl.
```

A descendant object could specialize the predicate using the following definition:

```logtalk
salutation :-
    ^^salutation,
    write('Long time, no see!), nl.
```

By preserving *self*, the *super call* ensures that the predicate `name/1` is called in the context of the object that received the `salutation/0` message, not in the context of the object making the *super call*.

But there's no concept of *self* in the `:/2` control construct (explicit module-qualified calls are not message sending calls). Thus, hacking a *super call* using a `:/2` goal requires either knowing that no inherited definition makes calls in *self* (and that such calls will never be added when maintaining the code) or making *self* explicit and passing it as an additional predicate argument.

P.S. The Logtalk distribution includes a programming example illustrating the semantics of *super calls*, including the requirement to preserve *self* and the support for dynamic predicates:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/super_calls](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/super_calls)

