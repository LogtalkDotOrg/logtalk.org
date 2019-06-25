---
layout: article
title: "Multifile predicates: dos and don'ts"
tags:
  - multifile
  - best practices
show_edit_on_github: false
aside: false
---

Multifile predicates are a standard Logtalk and Prolog feature. The name
*multifile* originates from being able to define a predicate in multiple
files. Multifile predicates are declared using a `multifile/1` directive.
For example:

```logtalk
:- multifile(foo/2).
```

Some Prolog systems only support dynamic multifile predicates. In those
cases, you will need to write:

```logtalk
:- multifile(foo/2).
:- dynamic(foo/2).
```

Logtalk and most Prolog systems also support multifile non-terminals. For
example:

```logtalk
:- multifile(bar//3).
```

Multifile predicates are as useful as problematic. On the positive side, a
multifile predicate can be used whenever you want to
add an extension point to your code. I.e. when you want to **provide some
default definition but still allow the user to plug in alternative definitions**.
For a simple and silly example, assume a `greetings/0` predicate that prints a
greetings message:

```logtalk
greetings :-
    write('Hello darling!').
```

All fine until you enter the taxicab and get a surprised stare from the driver.
Oops! After blushing, blaming lack of coffee, and an awkward ride, you rush to
your computer and change your code to:

```logtalk
:- multifile(greetings_hook/0).

greetings :-
    greetings_hook,
    !.
greetings :-
    write('Hello darling!').
```

You can now, depending on the social context, define the hook predicate to
output a more innocuous message when greeting strangers. For example:

```logtalk
:- multifile(greetings_hook/0).
greetings_hook :-
    write('Good morning!').
```

Of course, now that the door is open, a mischievous hacker (e.g. that friend
with an odd sense of humour) can add *another* hook definition:

```logtalk
:- multifile(greetings_hook/0).
greetings_hook :-
    write('Hi there sexy!').
```

Indeed, **multifile predicates are both extension and hacking points**. Always
take this into consideration.

But are you really in trouble? Depends. When using multifile predicates, you
should **never rely on the order of the multifile predicate clauses** as it
may depend on several factors including loading order and compiler implementation
details.

In more realistic scenarios, the hook predicates have some arguments that
simplify filtering which multifile predicate clauses apply. Rewriting our
greetings predicate:

```logtalk
:- multifile(greetings_hook/1).

greetings(Context) :-
    greetings_hook(Context),
    !.
greetings(_) :-
    write('Hello!').
```

And then:

```logtalk
:- multifile(greetings_hook/1).
greetings_hook(home) :-
    write('Hello darling!').
greetings_hook(outside) :-
    write('Good morning!').
...
```

Another common pattern is to call *all* multifile predicate definitions. For
example:

```logtalk
:- multifile(action_hook/1).

actions(Context) :-
    action_hook(Context),
    fail.
actions(_) :-
    default_actions.
```

All is well until a provider for the multifile predicate screams "This one is mine!"
and adds a cut to a clause:

```logtalk
:- multifile(action_hook/1).
action_hook(Context) :-
    !,
    ...
```

The nasty consequence in this case is that any other multifile predicate definitions
whose clauses happen to follow the one with the cut will never be called. Therefore,
**avoid cuts in multifile predicate definitions**. I.e. **avoid making assumptions about
the predicate calling the multifile predicate and about other multifile predicate
definitions**.

In the presence of Prolog modules or when using Logtalk objects, multifile predicates
can be declared and defined in modules and objects. In this case, there's an entity
that holds the multifile predicate *primary declaration* and other entities defining
clauses for the predicate. An example with objects (similar for modules minus the
`public/1` directive) could be:

```logtalk
:- object(foo).

    % primary declaration
    :- public(m/1)
    :- multifile(m/1).
    ...

:- end_object.
```

Other entities defining clauses for the multifile predicate, will need to prefix
the predicate functor with the name of the entity containing its primary declaration.
For example (in the case of a module, use instead the `:/1` operator):

```logtalk
:- object(bar).

    :- multifile(foo::m/1).
    foo::m(X) :-
        ...

:- end_object.
```

Note that **the body of a multifile predicate clause is compiled in the context of
the entity containing the clause**. In the example above, that means that the clause
for `foo::m/1` can call any predicate visible in the object `bar`. This is a notable
property as it allows us to provide a hook definition for a third-party component
while taking full advantage of local resources without otherwise exposing them.

Be aware that some permissive Prolog compilers allows a predicate to be forced
multifile without requiring a primary declaration. This provides an attack vector
that can be exploited by using `asserta/1` to add clauses before the original
ones of the hacked predicate. Logtalk prevents this issue by generating a compiler
error when the primary declaration is missing. 

Where to look for practical examples of using multifile predicates? In Logtalk,
look e.g. into the *message printing* and *question asking* [mechanisms](https://logtalk.org/manuals/userman/printing.html). In Prolog
systems, look e.g. for *message printing* and *term-expansion* mechanisms when
supported. 

P.S. The Logtalk compiler includes linter checks for missing `multifile/1` directives,
missing primary declarations, and multifile predicate clauses with cuts.
