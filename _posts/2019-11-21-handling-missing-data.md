---
layout: article
title: Handling missing data
tags:
  - best practices
show_edit_on_github: false
aside: false
---

Real world data is often faulty. Noisy data and missing data are common
problems that applications must deal with sensibly. In this blog post,
we focus on how to handle missing data. The solution we described can
also be used to handle noisy data.

As an example, assume our *raw data* is the set of facts that describe the
[Addams family](https://en.wikipedia.org/wiki/The_Addams_Family) in the
[`family`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/family)
example included in the Logtalk distribution:

```logtalk
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
```

The missing data in this case is the parents of Morticia and Gomez (plus the
parents of their parents, and ...). The first step in a data processing
application is the *data acquisition*. This can be as simple as reading
the data or apply some transformation to facilitate later processing. For
our purpose, assume that we want to convert the data to the following
representation:

```logtalk
% parents(Child, Father, Mother)
```

For the Addams children, the facts are straight-forward:

```logtalk
parents(pubert, gomez, morticia).
parents(pugsley, gomez, morticia).
parents(wednesday, gomez, morticia).
```

But how to represent the missing parents of Morticia and Gomez? Should we
use placeholder values like "Jane Doe" and "John Doe"? Should we throw an
error or print a warning for the missing data? Should we skip and discard
it? For all but the simplest cases, we want to **minimize the coupling between
*data acquisition* and *data processing***. I.e. we don't want to make any
hard choices during data acquisition that may constrain data processing.
Therefore, we need to represent the missing data in a way that allows
any later data processing to decide how to deal with it. Logtalk provides
an [`expecteds`](https://logtalk.org/library/library_index.html#expecteds)
library that allows convenient representation of the missing data:

```logtalk
parents(Person, ExpectedFather, ExpectedMother) :-
    % enumerate the persons in the family database
    (   male(Person)
    ;   female(Person)
    ),
    % construct expected terms that either hold the parent name or error information
    expected::from_goal((parent(Father,Person), male(Father)), Father, missing_father, ExpectedFather),
    expected::from_goal((parent(Mother,Person), female(Mother)), Mother, missing_mother, ExpectedMother).
```

The [`expected::from_goal(Goal, Value, Error, Expected)`](https://logtalk.org/library/expected_0.html#from-goal-4)
predicate constructs an *expected term* by calling `Goal` that binds
`Value` on success. Otherwise, it returns an expected term with the
unexpected goal error or failure represented by the `Error` argument.
I.e. **an expected term can be seen as an *opaque compound term* that either
holds a value or an error explaining why the value is missing**. Effectively,
**expected terms allows us to defer any error handling during the data
acquisition step to the data processing steps** where the data is actually
used.

How are expected terms used during *data processing*? Let's consider
two scenarios. In the first one, we want to print the names of all persons
and their parents with the names of missing parents replaced by either
`john doe` or `jane doe`:

```logtalk
print :-
    forall(
        (   parents(Person, ExpectedFather, ExpectedMother),
            % replace missing father or mother with hypothetical names
            expected(ExpectedFather)::or_else(Father, 'john doe'),
            expected(ExpectedMother)::or_else(Mother, 'jane doe')
        ),
        print(Person, Father, Mother)
    ).
```

The [`expected(Expected)::or_else(Value, Default)`](https://logtalk.org/library/expected_1.html#or-else-2)
predicate binds `Value` to the expected value when present.
Otherwise, it binds `Value` to the provided `Default`. Calling
the `print/0` predicate will output:

```text
gomez
  father: john doe
  mother: jane doe

pubert
  father: gomez
  mother: morticia

pugsley
  father: gomez
  mother: morticia

morticia
  father: john doe
  mother: jane doe

wednesday
  father: gomez
  mother: morticia
```

In the second data processing scenario, we want to print only the parent
records that are complete. Thus, we need to skip all records where the
mother and/or the father are unknown:

```logtalk
print_complete :-
    forall(
        (   data_acquisition::parents(Person, ExpectedFather, ExpectedMother),
            % fail if the father or the mother are unknown
            expected(ExpectedFather)::or_else_fail(Father),
            expected(ExpectedMother)::or_else_fail(Mother)
        ),
        print(Person, Father, Mother)
    ).
```

The [`expected(Expected)::or_else_fail(Value)`](https://logtalk.org/library/expected_1.html#or-else-fail-1)
binds `Value` to the to the expected value when present and fails
otherwise. The output of this predicate will be:

```text
pubert
  father: gomez
  mother: morticia

pugsley
  father: gomez
  mother: morticia

wednesday
  father: gomez
  mother: morticia
```

As we illustrated in these two simple scenarios, **each processing step can
individually and independently decide on how to handle missing that**.

Our Addams family example uses a single data acquisition step and multiple
but *parallel* processing steps. A different but also common scenario is a
*sequence* of processing steps. In this case, the handling of missing data
in one step is passed to the next step. Assume a children image processing
application that applies the following sequence of filters:

1. Crop to cat
2. Add bow tie
3. Make eyes sparkle
4. Make smaller
5. Add rainbow

The missing data in this could be no cat in the original raw image. But
there might be also a cat in the image with no visible head or with eyes
closed. For the sake of argument, assume the following possible filter
failures and their representation:

- No cat in the image; who let the cat out: `missing_cat`
- Cat trashed the bow tie; no funny business: `bow_tie_failure`
- Cat with eyes closed; no sparkling eyes: `eyes_closed`
- Cat enjoys lasagna; not the path to get smaller: `wants_to_grow`
- It is a sunny day; no rain for making rainbows: `sunny_day`

Testing for exceptions at each step would result in ugly code full of
conditionals masking what is essentially a simple sequence of steps.
But **expected terms can also be used to represent something that is
missing from a previous step, not just from the initial data acquisition
step**:

```logtalk
process_image(Image, Final) :-
    % encapsulate the "image" in an expected term
    expected::of_expected(Image, Final0),
    % apply a sequence of image filters
    crop_to_cat(Final0, Final1),
    add_bow_tie(Final1, Final2),
    make_eyes_sparkle(Final2, Final3),
    make_smaller(Final3, Final4),
    add_rainbow(Final4, Final5),
    % either return the final image or throw any exception
    % that happened while applying one of the filters
    expected(Final5)::or_else_throw(Final).
```

The idea is that **each processing step takes as input an expected term
and outputs an expected term**. At this point, of course, you're screaming
"DCGs!":

```logtalk
process_image(Image, Final) :-
    % encapsulate the "image" in an expected term
    expected::of_expected(Image, Final0),
    % apply a sequence of image filters
    phrase(process, Final0, Final1),
    % either return the final image or throw any exception
    % that happened while applying one of the filters
    expected(Final1)::or_else_throw(Final).

process -->
    crop_to_cat,
    add_bow_tie,
    make_eyes_sparkle,
    make_smaller,
    add_rainbow.
```

Either way, each processing step, i.e. each filter looks into the input
expected term and, if a value is present, does its task. If the value
is missing, that it simply passes the expected term to the next step. But if
for some reason a value is present but the task cannot be completed, it
outputs an expected term with that reason as the cause of the failure:
Using as example the first two filters:

```logtalk
crop_to_cat -->
    call(apply_filter(cropped, missing_cat)).

add_bow_tie -->
    call(apply_filter(with_bow_tie, bow_tie_failure)).

...
```

As this is just an example, we simplify our code by assuming that the same
`apply_filter/4` predicate could be used by all the filters. Moreover, just
for the sake of a demo output, we use the
[`random::maybe(Probability)`](https://logtalk.org/library/randomp_0.html#maybe-1)
predicate to decide between filter success or failure:

```logtalk
apply_filter(Filter, Error, In, Out) :-
    Filtered =.. [Filter, Value],
    expected(In)::flat_map(
        {Filtered,Error}/[Value,Expected]>>(expected::from_goal(maybe(0.9), Filtered, Error, Expected)),
        Out
    ).
```

The [`expected(Expected)::flat_map(Closure, NewExpected)`](https://logtalk.org/library/expected_1.html#flat-map-2)
predicate either simply returns the expected term if it contains an unexpected
error (thus passing it along the sequence of calls) or applies a closure to
the expected value and the resulting expected term. Here we use a
lambda expression to call the `from_goal/4` constructor, which takes as
arguments a goal whose success or failure/error dictates if we wrap an expected
value, `Filtered`, or an unexpected error, `Error`. Given the use of a
random number generator, the output would be something like:

```text
% call cascade::process_image/2 repeatedly to trigger the random errors:

| ?- cascade::process_image(image, Final).
Final = with_rainbow(smaller(sparkling_eyes(with_bow_tie(cropped(image))))).

| ?- cascade::process_image(image, Final).
uncaught exception: missing_cat

| ?- cascade::process_image(image, Final).
Final = with_rainbow(smaller(sparkling_eyes(with_bow_tie(cropped(image))))).

| ?- cascade::process_image(image, Final).
uncaught exception: eyes_closed

| ?- cascade::process_image(image, Final).
Final = with_rainbow(smaller(sparkling_eyes(with_bow_tie(cropped(image))))).

| ?- cascade::process_image(image, Final).
Final = with_rainbow(smaller(sparkling_eyes(with_bow_tie(cropped(image))))).

| ?- cascade::process_image(image, Final).
uncaught exception: sunny_day
```

But is there any advantage in this case to use expected terms instead of
simply calling the sequence of filters from a `catch/3` or `setup_call_cleanup/3`
goal and having all filters throw exceptions? Using exceptions for control
flow is not good practice, specially for declarative languages. Exceptions are
also relatively costly. Is easy, of course, to convert an exception into a
failure if necessary but at that point we are already paying the declarative
and computational price of using exceptions.

Assume we are processing a large set of images, triggering a significant number
of filter failures. Using expected terms, until the last goal in the body of
our `process_image/2` predicate, there are no exceptions being throw. We could
simply change the last goal to:

```logtalk
process_image(Image, Final) :-
    ...,
    expected(Final1)::or_else_fail(Final).
```

I.e. simply fail if one of the filters failed and move to the next image
in our processing pipeline. In this alternative, no exceptions are ever
generated.

Another possible advantage of using expected terms instead of a `catch/3`
or similar wrapper is that each step have the chance to fix a failure in
a previous step. But using exceptions results in aborting the sequence
of steps and jumping out to the exception handler with no chance of
locally recovering from a step failure and continuing to the next step.

Using expected terms also allows us to handle both step errors and failures
uniformly and simplify attaching *explanations* to failures as an unexpected
result is just a wrapped term. Using a `catch/3` or `setup_call_cleanup/3`
solution, a step that fails gives no explanation to the cause of the failure.
We could workaround this issue by forcing the use of exceptions to represent
any failures but this is far from ideal if the individual steps can be used
in other contexts where a failure is a preferred outcome.

Yet another possible advantage of expected terms is easier *composition* of
groups of processing steps. A failure or error can be simply passed from a
group of steps to another group of steps. We can choose, for exemple, to handle
exceptional events at a sigle place at the end of the processing pipeline.
If, in alternative, each group of steps is wrapped by a `catch/3` or
`setup_call_cleanup/3` goal, we easily end up with multiple exception handlers,
often nested, and worrying if we forgot to handle a particular exception or if
we captured an exception that should have been passed to an outer handler.

### Final notes

The use of expected terms give clear advantages in some cases, such as in
the family example, and possible advantages in other cases, such as in the
cats example. In the later case, consider carefully the inherent cost of
using expected terms (specially if wrapping built-in and library predicates
to convert variable bindings) and the desired semantics for handling exceptional
events (notably, the need for failure explanations and *fail fast* versus passing
the exceptional event along the processing pipeline).

The [`expecteds`](https://logtalk.org/library/library_index.html#expecteds)
library provides other useful predicates for constructing and handling
expected terms. The use of the
[`expected/1`](https://logtalk.org/library/expected_1.html) parametric
object enables static binding to be used for all calls to the predicates
that operate on expected terms for the best performance.

### Resources

The Logtalk distribution includes the full source code of the examples
used in this blog post: [`missing_data`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/missing_data)
and [`cascade`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/cascade).

Scott Wlaschin blog post and presentation on [Railway Oriented Programming](https://fsharpforfunandprofit.com/rop/).
