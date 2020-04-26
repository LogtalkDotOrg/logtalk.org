---
layout: article
title: Building trust on property-based testing
tags:
  - best practices
  - testing
show_edit_on_github: false
aside: false
---


This is the third blog post on *property-based testing*. For background, be
sure to read the 
[first](../../../2019/08/20/easily-quickcheck-your-predicates.html)
and [second](../../../2020/04/10/evolving-from-manually-written-tests.html)
posts.

Some of the common concerns from new users of property-based testing are:

- How can we trust a process that uses *randomly* generated tests?
- How can we ensure that both the typical cases and the edge cases that we usually test explicitly
using traditional unit tests will be among the randomly generated tests?
- How can be verify that the properties that we define are themselves bug free?


Ensuring that edge cases are tested
-----------------------------------

Edge cases are quite common and often obvious when we look to predicate
input arguments. If an argument is a list, is an empty list properly handled?
If another argument is an integer, does the predicate behaves correctly when
passed a zero? What about a negative integer? If a float argument must be in
a given range, are both the minimum and maximum values accepted?

The [`arbitrary`](https://logtalk.org/library/arbitrary_0.html)
library category defines default edge cases for common types, which we can
query via the [`type`](https://logtalk.org/library/type_0.html) object
(the category [*complements*](https://logtalk.org/manuals/userman/categories.html#hot-patching)
the object, adding new predicates to it). For example:

```text
| ?- type::edge_case(atom, Value).
Value = ''
yes

| ?- type::edge_case(byte, Value).
Value = 0 ? ;
Value = 255
yes

| ?- type::edge_case(list, Value).
Value = []
yes
```

Edge cases are tested before the [QuickCheck](https://logtalk3.readthedocs.io/en/latest/devtools/lgtunit.html#quickcheck)
implementation switches to
generating random tests. Their use is controlled by the `ec(Boolean)`
option for the `quick_check/2-3` predicates and [test dialects](https://logtalk3.readthedocs.io/en/latest/devtools/lgtunit.html#test-dialects).
Its default value is `true`. It can be set to `false` in those rares cases
where for some reason we want to disable the use of edge cases.

When the default edge cases don't provide the necessary coverage, e.g.
when defining new types and arbitrary value generators for those types,
we can add new edge cases by defining clauses for the
[`edge_case/2`](https://logtalk.org/library/arbitrary_0.html#edge-case-2)
multifile predicate. For example, assuming we are defining a new `age` type
with range `[0, 121]`: 

```logtalk
:- multifile(arbitrary::edge_case/2).
arbitrary::edge_case(age, 0).
arbitrary::edge_case(age, 121).
```

Although this is a simple example, the construction of edge cases may be
non-trivial computations. In any case, we can always QuickCheck the
`edge_case/2` definitions:

```text
| ?- lgtunit::quick_check(type::edge_case({age}, -between(integer,0,121))).
% 100 random tests passed, 0 discarded
% starting seed: seed(3172,9814,20125)
yes
```

The `{age}` notation tells QuickCheck that the argument have a fixed value.
The second argument uses the default `between/3` type to check that the
returned value is an integer in the valid range.


Labelling generated tests
-------------------------

Now that we know how to ensure that edge cases are tested, what about the
randomly generated tests? When writing traditional unit tests, is common
practice to cover typical cases. But can we get the same assurance using
property-based testing? The `quick_check/2-3` predicates and test dialects
support a `l(Closure)` option that allows us to label the generated tests.
For example, assume the following predicate definition:

```logtalk
label(List, _, Label) :-
    length(List, Length),
    (   Length mod 2 =:= 0 ->
        Label = even
    ;   Label = odd
    ).
```

In the [previous](../../../2020/04/10/evolving-from-manually-written-tests.html)
blog post, we used as example an `every_other/2` predicate that returns
every other element in the list. The
[original](../../../2019/08/20/easily-quickcheck-your-predicates.html)
buggy version wrongly assumed an input list with an even number of elements
and was diagnosed and fixed using QuickCheck. The fixed version is:

```logtalk
every_other([], []).
every_other([H| T], L) :-
    every_other(T, H, L).

every_other([], X, [X]).
every_other([_| T], X, [X| L]) :-
    every_other(T, L).
```

To ensure that QuickCheck is indeed generating tests using lists with
both an even and an odd number of elements, we can use the `label/3`
predicate by passing the option `l(label)`. The `label` closure will be
called, for each generated test, by appending the two predicate arguments
used by test call to the `every_other/2` predicate plus the labels
argument (the labelling predicate can return a single test label or a
list of test labels):

```text
| ?- lgtunit::quick_check(
         every_other(+list(integer), -list(integer)),
         [l(label), n(10000)]
     ).
% 10000 random tests passed, 0 discarded
% starting seed: seed(3172,9814,20125)
% even: 5112/10000 (51.120000%)
% odd: 4888/10000 (48.880000%)
yes
```

As the printed stats show, there's a reassuring balanced split between
lists with even and odd lengths. But is this enough? Note that we didn't
check e.g. that all elements in the output list are present in the input
list or that the size of the output list is half the size of the input
list. See our [previous](../../../2020/04/10/evolving-from-manually-written-tests.html)
post for a full example on defining properties for the predicates being
tested.


Restricting generated tests
---------------------------

Assume that we want to restrict the randomly generated tests to those
where the input list have an odd number of elements, which triggered
the bug in the
[original](../../../2019/08/20/easily-quickcheck-your-predicates.html)
definition of the `every_other/2` predicate.
We can use the `pc(Closure)` option for this purpose. The clousure will
work as a pre-condition and will be called, for each generated test, by
appending the two predicate arguments that would be used by the test.
If the call fails, the test is discarded and a new candidate test is
generated. Thus, with the following predicate definition:

```logtalk
condition(List, _) :-
    length(List, Length),
    Length mod 2 =:= 1.
```

we can call:

```text
| ?- lgtunit::quick_check(
         every_other(+list(integer), -list(integer)),
         [pc(condition), l(label), n(10000)]
     ).
% 10000 random tests passed, 10590 discarded
% starting seed: seed(9170,22060,20847)
% odd: 10000/10000 (100.000000%)
yes
```

Note that the number of discarded tests is close to the number of tests
that were run given that, as the previous query demonstrated, QuickCheck
generates a balanced split between lists of even and odd lengths.

We can also use similar pre-conditions to verify that our `label/3` predicate
is correctly labelling tests:

```logtalk
odd_list(List, _, _) :-
    length(List, Length),
	Length mod 2 =:= 1.

even_list(List, _, _) :-
    length(List, Length),
	Length mod 2 =:= 0.
```

```text
| ?- lgtunit::quick_check(label(+list, {[]}, {odd}), [pc(odd_list)]).
% 100 random tests passed, 109 discarded
% starting seed: seed(17567,8226,21714)
yes

?- lgtunit::quick_check(label(+list, {[]}, {even}), [pc(even_list)]).
% 100 random tests passed, 102 discarded
% starting seed: seed(22040,19096,13145)
true.
```

The `pc(Closure)` option is also useful when constraining or enforcing a
relation between the generated arguments and can sometimes be used as an
alternative to define custom types. See the `lgtunit` tool
[documentation](https://logtalk3.readthedocs.io/en/latest/devtools/lgtunit.html#quickcheck)
for further details and examples.

In actual cases, we can and often use QuickCheck itself and the solutions
illustrated in this blog post to verify that the properties that we write
to test predicates, plus the pre-conditions and labels that we use to filter
and classify tests, are correct.


**Note:** The `ec/1`, `l/1`, and `pc/1` options require the current Logtalk
[git version](https://github.com/LogtalkDotOrg/logtalk3) or the
forthcoming 3.38.0 release, expected to be available by end of April,
beginning of May.
