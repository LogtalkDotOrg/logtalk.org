---
title: Working with data sets
author: Paulo Moura
layout: article
tags: data
show_edit_on_github: false
aside: false
---

A recurring question on the [comp.lang.prolog](http://groups.google.com/group/comp.lang.prolog/topics) newsgroup is how to work with different data sets, usually loading them from different files, without mixing the data in the plain Prolog database. Unfortunately, these questions often lack enough details for making an informed choice between several potential programming solutions. Two possible solutions are (1) load the data into suitable data structures instead of using the database and (2) use clauses to represent the data but encapsulate each data set in its own Prolog module or Logtalk object. Some combination of both solutions may also be possible. In this post, however, we're going to sketch the second solution using Logtalk objects. For an alternative but also Logtalk-based solution please see [this previous post](../../02/15/efficient-representation-of-data-objects/).

Assuming all data sets are described using the same predicates, the first step is to declare these predicates. The predicate declarations can be encapsulated either in an object or in a protocol (interface). Using a protocol we could write:

```logtalk
:- protocol(data_set).

    :- public(datum_1/3).  % data set description predicates
    :- public(datum_2/5).
    ...

:- end_protocol.
```

We can now represent each data set using its own object (possibly stored in its own file). Each data set object implements the `data_set` protocol defined above. For example:

```logtalk
:- object(data_set_1,
    implements(data_set)).

    datum_1(a, b, c).
    ...

    datum_2(1, 2, 3, 4, 5).
    ...

:- end_object.
```

Assuming we have the required memory, we can load some of all of our data sets without mixing their data. But that's not all. We can also encapsulated our data set processing code in its own object (or set of objects, or hierarchy of objects, or whatever is suitable to the complexity of our application). This object, let's name it `processor`, will perform its magic by sending messages to the specific data set that we want to process. For example:

```logtalk
:- object(processor).

    :- public(compute/2).
    ...

    compute(DataSet, Computation) :-
        DataSet::datum_1(A, B, C),
        ...

:- end_object.
```

If the computations we wish to perform make sense as questions sent to the data sets themselves, an alternative is to move the data set predicate declarations from the `data_set` protocol to the `processor` object and make the data set objects extend the resulting object, below renamed as `data_set`. For example:

```logtalk
:- object(data_set).

    :- public(datum_1/3).  % data set description predicates
    :- public(datum_2/5).
    ...
    :- public(compute/1).  % computing predicates
    ...

    datum_3(abc, def).     % default value for datum_3/2

    compute(Computation) :-
        ::datum_1(A, B, C),
        ...

:- end_object.

:- object(data_set_1,
    extends(data_set)).

    datum_1(a, b, c).
    ...

    datum_2(1, 2, 3, 4, 5).
    ...

:- end_object.
```

An advantage of this solution is that the object `data_set` can contain default values for the data set description predicates. The `::/1` operator used above is the Logtalk operator for sending a message to _self_, i.e. to the data set object that received the message `compute/1`. If the information requested is not found in the data set object, then it will be looked for in its ancestor, where the default values are defined.

The best and most elegant solution will, of course, depend on the details on the data set processing application. For example, above we could have defined the object `data_set` as a class and the individual data sets as instances of this class (technically, the solution above uses prototypes).

Note that all code above is static. Individual data set description predicates may be declared dynamic (using the predicate directive `dynamic/1`) if we need to update them during processing of the data sets. If our application requires being able to delete data sets from memory, is simply a question of declaring the data set objects dynamic using the Logtalk object directive `dynamic/0` and to use the Logtalk built-in predicate `abolish_object/1` when a data set object is no longer needed. 

We have only scratched the surface of the Logtalk features that we could make use in our implementation but, hopefully, it's enough as a starting guide. Feel free to stop by the [Logtalk discussion forums](http://forums.logtalk.org) to further discuss this programming pattern.
