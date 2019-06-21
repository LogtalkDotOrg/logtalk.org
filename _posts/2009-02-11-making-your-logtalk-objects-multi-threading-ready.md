---
title: Making your Logtalk objects multi-threading ready
author: Paulo Moura
layout: article
tags:
  - threads
show_edit_on_github: false
aside: false
---

Even if you're not currently using Logtalk [high-level multi-threading support](https://logtalk.org/manuals/userman/threads.html) to speed up your application in your shining new multi-core hardware, it's quite easy to make your Logtalk objects and libraries multi-threading ready. Here's how:

First, locate all your objects defining predicates that have side-effects. For example, predicates that perform input/output operations or use the (object) dynamic database. Second, add [`synchronized/1`](https://logtalk.org/manuals/refman/directives/synchronized_1.html) directives for those predicates. Third, well, there is not third step.

A simple example, based on the Logtalk `gensym` library object:

```logtalk
:- public(gensym/2).
:- synchronized(gensym/2).

gensym(Base, Unique) :-
    retract(base_(Base, OldInt)) -&gt;
    asserta(base_(Base, NewInt)),
    number_codes(NewInt, NewCodes),
    atom_codes(NewAtom, NewCodes),
    atom_concat(Base, NewAtom, Unique).
```

Using the `synchronized/1` directive guarantees that two or more threads concurrently calling the `gensym/2` predicate will not step on each other's toes. Synchronized predicates are silently compiled as normal predicates when using back-end Prolog compilers that don't support multi-threading programming, so there's no penalty when running single-threaded.
