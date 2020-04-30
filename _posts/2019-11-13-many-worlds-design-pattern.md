---
layout: article
title: The "many worlds" design pattern
tags:
  - design patterns
  - best practices
show_edit_on_github: false
aside: false
---

The *many worlds* design pattern is one of the most common patterns in Logtalk
and Prolog applications. It allows reasoning about different worlds, where a
world can be e.g. a dataset, a knowledge base, a set of examples. While this
design pattern can be trivially implemented when only a single world is
defined at any single time, a solution allowing multiple worlds to be defined
concurrently is often desirable or required. Logtalk provides two sensible and
simple implementation solutions, using inheritance and parametric objects.

To illustrate this design pattern and its possible implementations, consider
the classic *family relations* example. In this case, we have basic facts
about each family member like sex and parents. From these facts, we want
to infer family relations such as father, mother, sister, or brother.
As concrete family examples, we're going to use the
[Addams family](https://en.wikipedia.org/wiki/The_Addams_Family) and the
[Simpson family](https://en.wikipedia.org/wiki/Simpson_family). You can blame
these choices on too much TV and movies growing up.

### Inheritance based solution

In this solution, we have a root object defining the family relations with
the concrete families defined as descendant objects. The implementation of
the family relations simply call the basic family facts by sending messages
to *self*:

```logtalk
:- object(family).

    :- public([
        father/2, mother/2, sister/2, brother/2
    ]).

    :- public([
        parent/2, male/1, female/1
    ]).

    father(Father, Child) :-
        ::male(Father),
        ::parent(Father, Child).

    mother(Mother, Child) :-
        ::female(Mother),
        ::parent(Mother, Child).

    sister(Sister, Child) :-
        ::female(Sister),
        ::parent(Parent, Sister),
        ::parent(Parent, Child),
        Sister \== Child.

    brother(Brother, Child) :-
        ::male(Brother),
        ::parent(Parent, Brother),
        ::parent(Parent, Child),
        Brother \== Child.

:- end_object.
```

We can now define e.g. the Addams family as a descendant object:

```logtalk
:- object(addams,
    extends(family)).

    male(gomez).
    male(pubert).
    male(pugsley).

    female(morticia).
    female(wednesday).

    parent(gomez, pubert).
    parent(gomez, pugsley).
    parent(gomez, wednesday).
    parent(morticia, pubert).
    parent(morticia, pugsley).
    parent(morticia, wednesday).

:- end_object.
```

Querying a family relation translates to a message to the family object.
For example:

```logtalk
| ?- addams::mother(Mother, Child).

Mother = morticia,
Child = pubert ;
Mother = morticia,
Child = pugsley ;
Mother = morticia,
Child = wednesday ;
no
```

An interesting variation of this implementation is to use a root category
instead of a root object. In this alternative, the concrete family objects
import the category instead of extending a root object. The advantage is
that it's no longer possible to send messages to the root entity itself
that could never be answered as it represents an abstraction. A more
classical solution is to define `family` as a class instead of a prototype
(or category) and to define concrete families like `addams` as class
instances. 

### Parametric object based solution

In this alternative solution we define the family relations in a parametric
object that takes as parameter an object implementing the basic facts for a
concrete family:

```logtalk
:- object(family(_Family_)).

    :- public([
        father/2, mother/2, sister/2, brother/2
    ]).

    :- uses(_Family_, [
        parent/2, male/1, female/1
    ]).

    father(Father, Child) :-
        male(Father),
        parent(Father, Child).

    mother(Mother, Child) :-
        female(Mother),
        parent(Mother, Child).

    sister(Sister, Child) :-
        female(Sister),
        parent(Parent, Sister),
        parent(Parent, Child),
        Sister \== Child.

    brother(Brother, Child) :-
        male(Brother),
        parent(Parent, Brother),
        parent(Parent, Child),
        Brother \== Child.

:- end_object.
```

In this case, the basic family facts are accessed by sending an (implicit)
message to the object passed as a parameter. Here is becomes convenient to
define a family protocol that any concrete family can implement:

```logtalk
:- protocol(family_basic_relations)

    :- public([
        parent/2, male/1, female/1
    ]).

:- end_protocol.
```

The Simpson family can be then represented by the following object:

```logtalk
:- object(simpson,
    implements(family_basic_relations)).

    male(homer).
    male(bart).

    female(lisa).
    female(maggie).
    female(marge).

    parent(homer, bart).
    parent(homer, lisa).
    parent(homer, maggie).
    parent(marge, bart).
    parent(marge, lisa).
    parent(marge, maggie).

:- end_object.
```

To query a concrete family, we send a message to the parametric object:

```logtalk
| ?- family(simpson)::father(Father, Child).

Father = homer,
Child = bart ;
Father = homer,
Child = lisa ;
Father = homer,
Child = maggie ;
no
```

### Comparing the solutions

**Scalability:** The definition of multiple concrete worlds is only limited
by the available memory in both solutions. The definiton of relations over
the basic facts to describe concrete worlds require the same effort.

**Extensibility:** In the inheritance based solution, any new relation that
we add to the `family` object becomes immediately available for use with the
concrete family objects. Likewise, in the parametric object based solution,
any new relation that we add to the `family/1` parametric object becomes
immediately available for querying concrete family objects. One advantage of
the inheritance based solution is that we can extend the root object and then
have concrete worlds derived from those extensions without changing the fact 
that queries are still sent to the concrete world objects. Doing the same
with the parametric object based solution would require sending queries about
concrete world objects to a different parametric object.

**Performance:** Both solutions use necessarily *dynamic binding*. In the case
of the inheritance based solution, we use messages to *self* as the concrete
family is only know at runtime. In the case of the parametric object based
solution, we send messages to a concrete family object (passed as a parameter)
that is also only known at runtime. For critical performance applications, a
third solution is possible using multifile predicates to enable *static binding*.
This multifile based solution requires, however, some boilerplate code and thus
forgoes the simplicity of the two main solutions detailed above.

### Resources

The Logtalk distribution includes a discussion of this design pattern in its
[`design_patterns`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/design_patterns)
example, including sample implementations. It also includes
[`family`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/family)
and [`family_alt`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/family_alt)
examples with the latter illustrating the third alternative solution using
multifile predicates mentioned above.
