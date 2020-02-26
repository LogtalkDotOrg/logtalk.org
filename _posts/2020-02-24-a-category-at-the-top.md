---
layout: article
title: A category at the top
tags:
  - best practices
  - categories
show_edit_on_github: false
aside: false
---

Logtalk supports both prototypes and classes/instances. While classes and instances
provide a clear distinction between *abstractions* and *materializations* of those
abstractions, prototypes are usually used to represent concrete, one of a kind entities.
But prototypes can also be derived from similar prototypes by stating what makes them
different from their parent prototypes. The
[`elephants`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/elephants) example ([videocast](https://asciinema.org/a/297030)) in the Logtalk
distribution nicely illustrates this idea. We start by representing Clyde, a typical
elephant, grey, and with four legs:

```logtalk
% clyde, our prototypical but also concrete elephant
:- object(clyde).

    :- public(color/1).
    color(grey).

    :- public(number_of_legs/1).
    number_of_legs(4).

:- end_object.
```

This is a fine representation if we have a single elephant or just a few elephants. But we
can have a rare albino elephant like Fred. We could represent it as a *standalone* prototype
like we did for Clyde. Or we can derive its representation from Clyde's representation:

```logtalk
% fred, another elephant, is like clyde, except that he's white
:- object(fred,
    extends(clyde)).

    % override inherited definition
    color(white).

:- end_object.
```

At this point we may start thinking: should we use classes and instances instead?
Instead of prototypes, we could have an `elephant` class with `clyde` and `fred` as
instances. The class could define default values for color and number for legs that
could be overriden in instances if necessary. Why use prototypes in the first place?
In general, how do we decide between using prototypes or classes?

One clear advantage of prototypes, already mentioned, is that they simplify representing
one of a kind entities. They are a trivial implementation of the *singleton* design
pattern. With classes, we would need to define a class, a single instance, and
possibly some solution for ensuring no other instances would be defined or created.
But then Fred or some other unique elephant could come stomp on our carefully written
code. With prototypes, there is no need to redo our class hierarchy. We just represent
what's different from an existing prototype as each prototype can have unique attributes.
E.g. an elephant named Rose with a cute birth mark:

```logtalk
% rose, an elephant, is like clyde, but with a cute birth mark
:- object(rose,
    extends(clyde)).

    :- public(birth_mark/1).
    birth_mark(heart_shaped).

:- end_object.
```

With classes, we would need to introduce subclasses for each unique attribute or each
combination of unique attributes. Here, [categories](https://logtalk.org/manuals/userman/categories.html)
could help avoid finding ourselves entangled with multiple inheritance and a
combinatorial explosion of subclasses (see e.g. the
[`points`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/points)
example). Still, classes work best when we can anticipate
all our representation requirements. Prototypes work best when exceptions are common
and unpredictable. Prototypes are also arguably simpler as there's a single relation,
*extends*, while with classes we have two relations, *instantiates* and *specializes*.
But we can find ourselves in a situation where we prefer prototypes and feeling envy of
class organizational features. For example, instead of having most new elephants derived
from `clyde`, or an ad hoc solution with elephants derived from diverse elephants, we
may want to define a *prototypical but abstract elephant* to declare and possibly define
common attributes like color, number of legs, or birth date. Trouble is, nothing would
prevent sending a message to that prototypical elephant even if nonsensical like birth
date, which is only defined for concrete elephants. The solution: a category at the top
that can be imported by any prototype (a category is a fine-grained, cohesive, set of
predicate declarations and definitions that can be imported by any number of objects).
We could, in some cases, use a protocol but a category allows us not only to declare
predicates but also provide default definitions for the predicates. In our example,
we could define:

```logtalk
:- category(elephant_commons).

    :- public(color/1).
    % default color
    color(grey).

    :- public(number_of_legs/1).
    % default number of legs
    number_of_legs(4).

    :- public(birth_date/1).
    % no default

:- end_category.
```

And then, redefine `clyde`, `fred`, and `rose` as follows:

```logtalk
:- object(clyde,
    imports(elephant_commons)).

:- end_object.


:- object(fred,
    imports(elephant_commons)).

    % override inherited definition
    color(white).

:- end_object.


:- object(rose,
    imports(elephant_commons)).

    :- public(birth_mark/1).
    birth_mark(heart_shaped).

:- end_object.
```

Given that we cannot send messages to categories, we don't need to be careful to avoid
a prototypical but abstract elephant when e.g. enumerating elephants and sending them
messages. Thus, by taking advantage of categories, we get some of the organizational
features of classes in a more lightweight and flexible solution that is more amenable
to unforeseen representation requirements.
