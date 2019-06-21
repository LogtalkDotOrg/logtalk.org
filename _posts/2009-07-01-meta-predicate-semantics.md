---
title: Meta-predicate semantics
author: Paulo Moura
layout: article
tags: semantics
show_edit_on_github: false
aside: false
---

Meta-predicates allow reusing of programming patterns. Encapsulating meta-predicates in Prolog modules or Logtalk objects allows client modules and objects to reuse predicates customized by calls to local predicates. Nevertheless, meta-predicate semantics differ between Prolog and Logtalk. Logtalk meta-predicate semantics are quite simple:

> Meta-arguments are always called in the meta-predicate calling context. The calling context is the object making the call to the meta-predicate.

Prolog semantics are similar but require the programmer to be aware of the differences between implicit and explicit module qualification. Consider the following meta-predicate library:

```logtalk
:- module(library, [my_call/1]).

:- meta_predicate(my_call(:)).
my_call(Goal) :-
    write('Calling: '), writeq(Goal), nl, call(Goal).

me(library).
```

A simple client could be:

```logtalk
:- module(client, [test/1]).

:- use_module(library, [my_call/1]).

test(Me) :-
    my_call(me(Me)).

me(client).
```

A simple test query:

```text
?- client:test(Me).
Calling: client:me(_G230)
Me = client.
```

This is the expected result, so everything seems nice and clear. But consider the following seemingly innocuous changes to the `client` module:

```logtalk
:- module(client, [test/1]).

test(Me) :-
    library:my_call(me(Me)).

me(client).
```

In this second version we use explicit qualification in order to call the `my_goal/1` meta-predicate. Repeating our test query gives:

```text
?- client:test(Me).
Calling: library:me(_G230)
Me = library.
```

In order to understand this result, we need to be aware that the `:/2` operator both calls a predicate in another module and changes the calling context of the predicate to that module. The first use is expected. The second use is not obvious, is counterintuitive, and often not properly documented. We can, however, conclude that the meta-predicate definition is still working as expected as the calling context is set to the `library` module. If we still want the `me/1` predicate to be called in the context of the `client` module instead, we need to explicitly qualify the meta-argument by writing:

```logtalk
test(Me) :-
    library:my_call(client:me(Me)).
```

This is an ugly solution but it will work as expected. Note that the idea of the `meta_predicate/1` directive is to avoid the need for explicit qualifications in the first place. But that requires using `use_module/1-2` directives for importing the meta-predicates and implicit qualification when calling them.

Explicit qualification is not an issue in Logtalk, nor does it change the calling context of a meta-predicate. Explicit qualification of a meta-predicate call sets where to start looking for the meta-predicate definition, not where to look for the meta-arguments definition.

I suspect that the contrived semantics of the `:/2` operator is rooted in optimization goals. When a directive `use_module/1` is used, most (if not all) Prolog compilers require the definition of the imported module to be available (thus resolving the call at compilation time). However, that doesn't seem to be required when compiling an explicitly qualified module call. For example, using SWI-Prolog 5.7.10 or YAP 6.0, the following code compiles without errors or warnings (despite the fact that the module `xpto` doesn't exist):

```logtalk
:- module(foo, [bar/0]).

bar :-
    xpto:blabla.
```

Thus, in this case the `xpto:blabla` call is resolved at runtime. In our example above with the explicit call to the `my_call/1` meta-predicate, the implementation of the `:/2` operator propagates the module prefix to the meta-arguments. Doing otherwise would imply knowing at runtime the original module containing the call, information that most Prolog compilers don't keep.

In the case of Logtalk, the execution context of a predicate call always includes the calling context, allowing simpler meta-predicate semantics (and much more). Moreover, the Logtalk compiler doesn't need to know that we're calling a meta-predicate when compiling source code. This allows client code to be compiled independently of library code. Meta-predicate information is either used at compile time when static binding is possible or at runtime. In the second case, the caching mechanism associated with dynamic binding ensures that the necessary computations to know which arguments are meta-arguments are only performed once. There is, of course, a small performance penalty in carrying predicate execution context. I argue that's a small price to pay in order to simplify meta-predicate semantics.
