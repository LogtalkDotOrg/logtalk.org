---
layout: article
title: Easily QuickCheck your predicates
tags:
  - tools
  - testing
show_edit_on_github: false
aside: false
---

Logtalk [`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html) testing tool includes a **[QuickCheck](https://en.wikipedia.org/wiki/QuickCheck) implementation** supporting property-based testing of plain Prolog, Prolog module, and Logtalk code. The tool is **portable and can be used with all Logtalk supported Prolog compilers**. The QuickCheck implementation provides specific unit test dialects and a set of predicates that can be used from anywhere, including at the top-level interpreter. Usage is simple and can be illustrated with some examples. Assume the following broken predicate definition: 

```logtalk
every_other([], []). 
every_other([_, X| L], [X | R]) :- 
    every_other(L, R). 
```

The predicate is supposed to construct a list by taking every other element of an input list. Cursory testing may fail to notice the bug: 

```text
?- every_other([1,2,3,4,5,6], List). 
List = [2, 4, 6]. 
```

How do we QuickCheck the predicate for stronger testing? Assuming Logtalk is already installed, we start by loading the `lgtunit` tool: 

```text
?- {lgtunit(loader)}. 
... 
```

The `lgtunit::quick_check/1` predicate takes a predicate property (or [signature](https://logtalk.org/manuals/userman/predicates.html#mode-directive)) and runs random generated tests (100 by default). Here we specify `list(integer)` argument types simply to simplify the results:

```text
?- lgtunit::quick_check(every_other(+list(integer), -list(integer))).
*     quick check test failure (at test 2 after 0 shrinks):
*       every_other([0],A)
false.
```

QuickCheck reports that the predicate fails for a list with a single element. Effectively, the predicate definition is assuming an input list with an even number of elements. After finding a counter-example, the QuickCheck implementation tries to shrink it in order to report the most simple counter-example possible to facilitate debugging (not performed as not required, however, in this simple example).

There's also a `lgtunit::quick_check/2` predicate that allows us to specify the number of tests (100 by default) and the maximum number of shrink operations (64 by default). To illustrate these options, consider the simple example of a predicate, `foo/1`, that succeeds when all elements on (a possibly empty) list are even:

```logtalk
foo([]). 
foo([N| _]) :- N mod 2 =:= 0.
```

It's quite obvious that this predicate will fail for any list containing an odd integer but the interesting point is what happens when a counter-example is found. To illustrate, we specify a maximum of 42 generated tests and a maximum of 10 shrink operations when a counter-example is found: 

```text
?- lgtunit::quick_check(foo(+list(integer)), [n(42), s(10)]).
*     quick check test failure (at test 5 after 7 shrinks):
*       foo([1])
false.
```

Note that, after finding a counter-example on the 5th generated random test, the QuickCheck implementation was able to shrink it 7 times. Without shrinking, the counter-example would be needlessly more complex:

```text
?- lgtunit::quick_check(foo(+list(integer)), [n(42), s(0)]).
*     quick check test failure (at test 3 after 0 shrinks):
*       foo([-651,-101,554,-551,41,836,443,695,917,932,-933,546,569,-740])
false.
```

In practical cases, successful shrinking results in simpler counter-examples that would be used as debugging starting points.

Let's now move from plain Prolog predicates to module predicates using a key-value pairs library found in some Prolog systems. 

```text
?- use_module(library(pairs)). 
true. 

?- lgtunit::quick_check(pairs_keys_values(+list(pair(atom,integer)),-list(atom),-list(integer))). 
% 100 random tests passed 
true. 
```

There is also a `lgtunit::quick_check/3` predicate that returns results in reified form. For example:

```text
?- lgtunit::quick_check(foo(+list(integer)), Result, [n(42), s(10)]).
Result = failed(foo([1])).

?- lgtunit::quick_check(pairs_keys_values(+list(pair(atom,integer)),-list(atom),-list(integer)), Result, []).
Result = passed.
```

For details about the `lgtunit::quick_check/1-3` predicates (and the QuickCheck test idioms), see the `lgtunit` tool [documentation](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md).

A special syntax for predicate signatures is worth mention. In some cases, we need to fix one or more input arguments instead of generating random values for them. For example, assume that we want to check that the defined shrinkers produce valid values. We can accomplish this using the query:

```text
?- forall((type::shrinker(Type), ground(Type)), lgtunit::quick_check(shrink_value({Type}, -Type))).
true.
```

The `{}/1` handy notation allow us to pass an argument value as-is, avoiding in this case the need of defining an auxiliary predicate to fix the argument.

For use in the predicate property/signatures, the Logtalk library (as of release 3.28.0) makes available 92 types (several of them parameterizable), can generate arbitrary (random) values for 79 of those types, and is able to shrink values for 54 types. The type definitions, random type value generators, and shrinkers are defined in the [`type`](https://logtalk.org/library/type_0.html) and [`arbitrary`](https://logtalk.org/library/arbitrary_0.html) library entities, which are user-extensible using multifile predicates.

Another noteworthy feature of the Logtalk QuickCheck implementation is the support for testing any defined **type edge cases** (e.g. `0` or `[]` or `''`). Currently, 79 edge cases for common types are defined by default. These edge cases are tried before resorting to generating random values. This helps prevent the otherwise random nature of of QuickCheck testing missing those edge cases that often expose bugs in the predicates being tested. The user can easily define additional edge cases using a multifile predicate.

If you type a few QuickCheck queries at the top-level interpreter to check your code, don't let those queries be wasted. The `lgtunit` tool support for QuickCheck test dialects allows you to easily saved those queries to a test set. As an example, the queries above could be used to define the following test set:

```logtalk
:- object(my_tests,
    extends(lgtunit)).

    quick_check(
        every_other_01,
        user:every_other(+list(integer), -list(integer))
    ).

    quick_check(
        foo_01,
        user:foo(+list(integer)),
        [n(42), s(10)]
    ).

    quick_check(
        pairs_pairs_keys_values_3,
        pairs:pairs_keys_values(+list(pair(atom,integer)),-list(atom),-list(integer))
    ).

:- end_object.
```

QuickCheck tests don't replace traditional unit tests but can offer significant and complementary advantages. Notably, they allow you to focus on the properties of predicate and set of predicates, thus working at a semantically higher level, and make the computer work for you by automatically generating tests instead of requiring the manual and laborious task of hand-writing tests. Moreover, the automatic shrink of any found counter-example provides a debugging starting point, contributing to faster development cycles.
