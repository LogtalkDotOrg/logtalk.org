---
title: Writing unit tests in Logtalk
author: Paulo Moura
layout: article
tags:
  - testing
show_edit_on_github: false
aside: false
---

Logtalk provides simple but portable support for writing unit tests. This support is provided by a library object, `lgtunit`, inspired on the works of Joachim Schimpf (ECLiPSe library `test_util`) and Jan Wielemaker (SWI-Prolog `plunit` package). You can load it using the goal:

```text
| ?- logtalk_load(library(lgtunit)).
```

The interface of the `lgtunit` object is quite simple and can be found e.g here:

[https://logtalk.org/library/lgtunit_0.html](https://logtalk.org/library/lgtunit_0.html)

Most of the examples found on the current Logtalk distribution include a set of unit tests, together with a handy loader file named `tester.lgt`. Typically, this loader file loads the code you want to test, the unit test framework, the unit tests themselves, and send a `run/0` message to the unit test objects. Check, for instance, the example:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/people](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/people)

In order for you to write your own unit tests, start by defining objects extending the `lgtunit` object. These objects must be compiled using the option `hook(lgtunit)`. For example:

```text
| ?- logtalk_load(my_tests, [hook(lgtunit)]).
```

After successful compilation and loading of your unit test objects, you can run them by typing:

```text
| ?- my_tests::run.
```

Logtalk unit tests can be written using any of three different dialects. The most simple dialect is:

```logtalk
test(Test) :- Goal.
```

This dialect allows the specification of tests that are expected to succeed. Tests that are expected to fail can be written by using the `\+/1` built-in predicate. However, tests that are expected to throw an error cannot be specified. A second dialect overcomes this restriction:

```logtalk
succeeds(Test) :- Goal.
fails(Test) :- Goal.
throws(Test, Error) :- Goal.
```

This is a straightforward dialect. For `succeeds/1` tests, `Goal` is expected to succeed. For `fails/1` tests, `Goal` is expected to fail. For `throws/2` tests, `Goal` is expected to throw `Error`. A third supported dialect is:

```logtalk
test(Test, Outcome) :- Goal.
```

In this case, `Outcome` can be the atom `true`, the atom `fail`, or the exception term that the test is expected to throw. In all cases, `Test` is an atom, uniquely identifying a test. Simply use the dialect that is the best fit for your application.

That's all. Happy testing!

**Note:** when using the `<</2` control construct to access and test an object internal predicates, make sure that the objects are compiled with the `context_switching_calls` flag set to `allow`.
