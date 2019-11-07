---
layout: article
title: User-defined test dialects
tags:
  - testing
  - best practices
show_edit_on_github: false
aside: false
---

Testing is a fundamental part of software development. Follows that writing
tests should be as accessible as possible. Although automatic test generation
is an established practice (using e.g. a [Quickcheck](../../08/20/easily-quickcheck-your-predicates.html)
implementation such as the one provided by Logtalk), tests are often manually
written. Thus, anything that gets in the way of expressing what we want to
test hurts productivity.

Testing tools such as [`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html)
aim to simplify writing tests by providing support for [multiple test dialects](https://logtalk.org/manuals/devtools/lgtunit.html#test-dialects)
where the programmer can choose from a minimal dialect, where we have only
a test name and a test goal, to a dialect offering fine control on test setup.
But that's not enough. People writing tests are not necessarily programmers.
Notably, they can be domain experts that want a straight-forward solution
to express that "for these inputs, we should get this output" or "if this
happens, this should be triggered" without having to learn a programming
language and its developer tools. The solution? Define a DSL for writing
tests and take advantage of `lgtunit` support for [user-defined test dialects](https://logtalk.org/manuals/devtools/lgtunit.html#user-defined-test-dialects).

Let's look into a simple but complete example. Assume that we're testing
an application that uses a predicate that takes three floating-point values
as input and generates an atom. The domain experts want to be able to write
tests using the following notation:

```logtalk
{12.7, 3.89, 5.67} => open_valve.
{2.04, 1.23, 0.77} => close_valve.
{20.4, 2.91, 6.97} => open_valve.
...
```

The notation is nice and clear and abstracts all details irrelevant for
the domain experts, including the name of the predicate being tested and
how to call it.

The first step is to define an object, implementing the
[`expanding`](https://logtalk.org/library/expanding_0.html)
protocol, that will convert the facts above into one of the supported
test dialects. For simplicity, we're going to assume that the
predicate being tested is named `app::compute/4`:

```logtalk
:- object(test_dsl,
    implements(expanding)).

    :- public(op(1200, xfx, =>)).

    :- uses(gensym, [gensym/2, reset_gensym/1]).
    :- uses(os, [decompose_file_name/4]).

    term_expansion(
        begin_of_file,
        [begin_of_file, (:- object(Name, extends(lgtunit)))]
    ) :-
        logtalk_load_context(source, Source),
        decompose_file_name(Source, _, Name, _),
        reset_gensym(t).

    term_expansion(
        ({A, B, C} => D),
        (test(Test, true(R == D)) :- app::compute(A, B, C, R))
    ) :-
        gensym(t, Test).

    term_expansion(
        end_of_file,
        [(:- end_object), end_of_file]
    ).

:- end_object.
```

Using the `test_dsl` object as an hook object to expand a data file
with `=>/2` facts results in the generation of a tests object named
after the data file. But how do we run the tests? As test objects
must be compiled using `lgtunit` as the hook object, we simply chain
the two hook objects. Assuming the `=>/2` facts are defined in a
`tests.data` file, a suitable `tester.lgt` driver file for the tests
would be:

```logtalk
:- op(1200, xfx, =>).

:- initialization((
    set_logtalk_flag(report, warnings),
    logtalk_load([
        lgtunit(loader),
        gensym(loader),
        os(loader),
        hook_flows(loader),
        app,
        test_dsl
    ]),
    logtalk_load(
        'tests.data',
        [hook(hook_pipeline([test_dsl,lgtunit]))]
    ),
    tests::run
)).
```

As an usage example, assuming the contents of the `tests.data` file
are the `=>/2` facts above and that we only have a placeholder for
the test predicate defined as:

```logtalk
:- object(app).

    :- public(compute/4).
    compute(_, _, _, open_valve).

:- end_object.
```

we will get:

```text
?- {tester}.
% 
% tests started at 2019/11/5, 14:45:22
% 
% running tests from object tests
% file: /Users/pmoura/test_dsl/tests.data
% 
% t1: success
!     t2: failure 
!       test assertion failed: open_valve==close_valve
!       in file tests.data between lines 2-2
% t3: success
% 
% 3 tests: 0 skipped, 2 passed, 1 failed
% completed tests from object tests
% 
% no code coverage information collected
% tests ended at 2019/11/5, 14:45:22
% 
true.
```

Note that the line numbers in the failed tests reflect the line of
the original `=>/2` fact.

The solution we described is easily applied to any user-defined test
dialect. Thus, anytime you find the predefined test dialects not ideal
for a particular application, consider simply defining your own custom
test dialect.
