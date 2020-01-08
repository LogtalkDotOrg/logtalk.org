---
layout: article
title: Object and predicate aliases
tags:
  - best practices
show_edit_on_github: false
aside: false
---

Naming is a non-trivial problem in programming. A good name conveys meaning,
contributing to code readability. But there's always a natural contention
between descriptive names and concise names that help avoid excess verbosity.
What's a good name may also depend on its usage context. Moreover, if every
library developer always use the best names, conflicts are bound to occur.
The usual solution to these issues is to support renaming of object, module,
and predicate names where they are used.

### Object aliases

The [`uses/1`](https://logtalk.org/manuals/refman/directives/uses_1.html)
directive can be used to declare object aliases when the programmer prefers
explicit message sending but also wants to use shorter names to minimize
verbosity. For example, Logtalk provides a `random` library with multiple
implementations of the same protocol, `randomp`. One of those implementations
is named `backend_random` as it's based on the backend Prolog compiler random
number generator. It also provides two portable implementations, `fast_random`
and `random`. We can use an object alias to both shorten the name and simplify
experimenting with the different implementations:

```logtalk
:- object(foo).

    :- uses([
        backend_random as rnd
    ]).

    bar :-
        ...,
        % the same as backend_random::permutation(L, P)
        rnd::permutation(List, Permutation),
        ...
```

To experiment with a different implementation of the `randomp` protocol,
we just need to change the `rnd` object alias definition and recompile.

Object aliases are specially useful using parametric objects. For example,
assume a library `time/1` parametric object where the parameter is the time
zone:

```logtalk
:- object(foo).

    :- uses([
        time('UTC−01:00') as time
    ]).

    bar :-
        ...,
        % the same as time('UTC−01:00')::now(Now)
        time::now(Now),
        ...
```

In this case, we bind the parameter in a single place in the code,
ensuring consistency while simplifying usage and maintenance. This
also works nicely for runtime bound parameters. For example, we can
also write:

```logtalk
:- object(foo(_HeapOrder_, _OptionsObject_)).

    :- uses([
        heap(_HeapOrder_) as heap,
        _OptionsObject_ as options
    ]).

    bar :-
        ...,
        % the same as heap(_HeapOrder_)::as_heap(List, Heap)
        heap::as_heap(List, Heap),
        % the same as _OptionsObject_::get(ratio, Ratio)
        options::get(ratio, Ratio),
        ...
```


### Predicate aliases

Predicate aliases provide similar benefits to object aliases but also allow
solving name clashes. Unlike in current Prolog modules practice where a
predicate name (e.g. `member/2`) is usually the exclusive of a specific
module (e.g. `lists`) with other modules forced to use different names
(e.g. `random_member/2`), library object predicates always use the best names.

The [`uses/2`](https://logtalk.org/manuals/refman/directives/uses_2.html)
directive can be used to declare object aliases for implicit message sending
while also solving name conflicts.
For example:

```logtalk
    :- uses(btrees, [new/1 as new_btree/1]).
    :- uses(queues, [new/1 as new_queue/1]).
    
    btree_to_queue :-
        ...,
        % the same as btrees::new(Tree)
        new_btree(Tree),
        % the same as queues::new(Queue)
        new_queue(Queue),
    ...
```

Name clashes also occur when using multiple inheritance. For example, assume
two objects, `rpg_player` and `engineer`, both declaring a `rank/1` public
predicate, and a third object, `moms_basement_ghost`, inheriting from the first
two objects. In this case, we can use the [`alias/2`](https://logtalk.org/manuals/refman/directives/alias_2.html)
directive to provide access to both inherited predicates by giving them
different aliases:

```logtalk
:- object(moms_basement_ghost,
    extends((rpg_player, engineer))).

    :- alias(rpg_player, [rank/1 as rpg_rank/1]).
    :- alias(engineer,   [rank/1 as engineer_rank/1]).

    rpg_rank(wizard).

    engineer_rank(senior).

:- end_object.
```

These aliases directives make possible the queries:

```text
| ?- moms_basement_ghost::rpg_rank(Rank).

Rank = wizard
yes

| ?- moms_basement_ghost::engineer_rank(Rank).

Rank = senior
yes
```

As a side note, we can still use `rank/1` as message. In this case, the default
multiple inheritance conflict solver would use the definition, if any, inherited
from the `rpg_player` object as it's listed first in the `moms_basement_ghost`
object opening directive.

Another common use of predicate aliases is to define an alternative predicate
name simply to make it more clear in its usage context. For example, assume a
`sentences` object exporting a `transpose//0` non-terminal:

```logtalk
    % define an alternative name for a non-terminal:
    :- alias(sentences, [transpose//0 as flip//0]).
```

Logtalk 3.34.0 added support for defining predicate shorthands where one
or more arguments can be omitted by binding the arguments in the original
predicate call template. For example:

```logtalk
    :- uses(logtalk, [
        print_message(debug, my_app, Message) as dbg(Message)
    ]).

    bar :-
        ...,
        % same as logtalk::print_message(debug, my_app, @oh_no)
        dbg(@oh_no),
        ...
```


Logtalk version of the [`use_module/2`](https://logtalk.org/manuals/refman/directives/use_module_2.html)
directive also provides similar support for defining predicate aliases and
shorthands. For example:

```logtalk
:- object(foo(_OptionsModule_)).

    :- use_module(_OptionsModule_, [
        set/2, get/2, reset/0
    ])

    :- use_module(pairs, [
        map_list_to_pairs(length, Lists, Pairs) as length_pairs(Lists, Pairs)
    ]).

    ...
```

### Final notes

Object and predicate aliases and shorthands can improve code readability,
consistency, and maintenance. They also make experimenting with alternatives
implementations easier by providing a single point of change. But they should
also be used with some care as any reading and understanding of source code,
specially long object definitions, must always take into account any defined
aliases and shorthands.
