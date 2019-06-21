---
title: Efficient representation of data objects
author: Paulo Moura
layout: article
tags:
  - proxies
  - best practices
show_edit_on_github: false
aside: false
---

Some Logtalk applications need to represent large numbers of immutable objects. These objects typically represent data that must be validated or used for data mining. This kind of data is often exported from databases and must be converted into Logtalk objects for further processing. The application logic is usually represented by a set of hierarchies with the data objects at the bottom. Although data conversion is most of the time easily scriptable, the resulting objects can take up significantly more space than a straightforward representation as Prolog facts. Logtalk object representation is simply not optimized for this kind of objects. Fortunately, this is one of those cases where you can eat the cake and keep it. The solution is to represent data as compact Prolog facts _and_ to interpret those facts as _object proxies_. An object proxy is simply a Prolog compound term that can be interpreted as a possible _instantiation_ of the identifier of a parametric object.

For a toy example, assume that your data represents geometric circles with attributes such as the circle radius and the circle color:

```logtalk
% circle(Id, Radius, Color)
circle('#1', 1.23, blue).
circle('#2', 3.71, yellow).
circle('#3', 0.39, green).
circle('#4', 5.74, black).
circle('#5', 8.32, cyan).
```

We can define the following parametric object for representing circles:

```logtalk
:- object(circle(_Id, _Radius, _Color)).

    :- public([
        id/1, radius/1, color/1,
        area/1, perimeter/1
    ]).

    id(Id) :-
        parameter(1, Id).

    radius(Radius) :-
        parameter(2, Radius).

    color(Color) :-
        parameter(3, Color).

    area(Area) :-
        ::radius(Radius),
        Area is 3.1415927*Radius*Radius.

    perimeter(Perimeter) :-
        ::radius(Radius),
        Perimeter is 2*3.1415927*Radius.

:- end_object.
```

The `circle/3` parametric object provides a simple solution for encapsulating a set of predicates associated with a given compound term. But how do we perform computations with the object proxies? We cannot send messages to Prolog facts! Or can we? Logtalk provides a handy notation for working with object proxies. For example, in order to construct a list with all circle areas we can write:

```logtalk
| ?- findall(Area, {circle(_, _, _)}::area(Area), Areas).

Areas = [4.75291, 43.2412, 0.477836, 103.508, 217.468]
yes
```

The message sending control construct, `::/2`, accepts as receiving object the term `{Proxy}`. Logtalk proves `Proxy` as a Prolog goal and, if successful, sends the message to the resulting term. Backtracking over the `Proxy` goal is supported, allowing all matching object proxies to be processed by a simple failure-driven loop (as implicit in the `findall/3` call above).

You can find the full source code of [this](http://svn.logtalk.org/viewvc.cgi/trunk/examples/proxies/) example in the current Logtalk distribution. In real applications, data objects, represented as object proxies, are tied to large hierarchies representing both knowledge about data and how to reason with it.
