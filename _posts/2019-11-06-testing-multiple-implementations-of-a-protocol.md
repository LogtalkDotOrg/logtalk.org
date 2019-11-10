---
layout: article
title: Testing multiple implementations of a protocol
tags:
  - testing
  - best practices
show_edit_on_github: false
aside: false
---

Testing multiple implementations of a protocol is a recurrent task. For
example, we may have multiple datasets that we need to check for integrity.
Or we may want to check multiple implementations of an abstract data type.
In this blog post, we will use Logtalk's
[`dictionaries`](https://logtalk.org/library/library_index.html#dictionaries)
library to illustrate how the Logtalk language features and the
[`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html) tool greatly
simplify this common task.

The `dictionaries` library defines a *dictionary* [protocol](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/dictionaries/dictionaryp.lgt)
(also known as a *map* or *associative array*) and three different [implementations](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/dictionaries/): a naive
implementation using a binary tree, a red-black tree implementation, and an
AVL tree implementation. The [tests](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/dictionaries/tests.lgt)
are necessarily the same and independent of the details of a particular
implementation. Therefore, the tests need to take as a parameter the
particular implementation being tested. This is easily accomplished by
using a parametric object:

```logtalk
:- object(tests(_DictionaryObject_),
    extends(lgtunit)).

    ...

:- end_object.
```

This allows us to run e.g. the tests for the AVL tree implementation provided
by the [`avltree`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/dictionaries/avltree.lgt)
object using the query:

```text
?- tests(avltree)::run.
```

The object parameter, `_DictionaryObject_`, is a *parameter variable* and its
semantics are simple: the compiler unifies the parameter with any occurrence
of the parameter variable within the object. For example:

```logtalk
test(dictionary_next_4_01) :-
    _DictionaryObject_::as_dictionary([], Dictionary),
    \+ _DictionaryObject_::next(Dictionary, _, _, _).
```

But this is verbose, specially when writing a large number of tests. We can
take further advantage of the parameter variable to simplify the tests by
using implicit message sending for all the predicates being tested:

```logtalk
:- uses(_DictionaryObject_, [
    as_dictionary/2, as_list/2,
    clone/3, clone/4, insert/4, delete/4, update/4, update/5, empty/1,
    lookup/3, previous/4, next/4, min/3, max/3, delete_min/4, delete_max/4,
    keys/2, values/2, map/2, map/3, apply/4, size/2, valid/1, new/1
]).
```

Thanks to this [`uses/2`](https://logtalk.org/manuals/refman/directives/uses_2.html)
directive, the test above can be simplified to:

```logtalk
test(dictionary_next_4_01) :-
    as_dictionary([], Dictionary),
    \+ next(Dictionary, _, _, _).
```

The only detail missing is how to run the tests for all dictionary implementations:

```text
?- lgtunit::run_test_sets([tests(avltree), tests(bintree), tests(rbtree)]).
```

The [`lgtunit::run_test_sets/1`](https://logtalk.org/library/lgtunit_0.html#run-test-sets-1)
predicate conveniently generates a single [code coverage report](https://logtalk.org/files/blog/2019_11_06/coverage_report.html) for all the
implementations and also allows generating a single [TAP report](https://logtalk.org/files/blog/2019_11_06/tap_report.txt) or [xUnit report](https://logtalk.org/files/blog/2019_11_06/xunit_report.html).
When the protocol implementations are only know at runtime, we can easily
construct a list of all the implementations by using the
[`implements_protocol/2-3`](https://logtalk.org/manuals/refman/predicates/implements_protocol_2_3.html)
and [`conforms_to_protocol/2-3`](https://logtalk.org/manuals/refman/predicates/conforms_to_protocol_2_3.html)
reflection predicates. For example, we can rewrite the query above as:

```text
?- findall(tests(Object), implements_protocol(Object,dictionaryp), Sets),
   lgtunit::run_test_sets(Sets).
```

##### NOTES

See the [`dictionaries`](https://logtalk.org/library/library_index.html#dictionaries)
library directory for the actual [`tester.lgt`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/dictionaries/tester.lgt)
driver file that is used for running the tests.

The XML files for the code coverage and the xUnit reports were generated
using the commands:

```bash
$ cd $HOME/logtalk/library/dictionaries
$ logtalk_tester -f xunit -c xml
```

The HTML version of the code coverage report linked above was then generated
using the commands:

```bash
$ cd $HOME/logtalk/library/dictionaries
$ xsltproc \
  --stringparam prefix logtalk/ \
  --stringparam url https://github.com/LogtalkDotOrg/logtalk3/tree/aa18ac872371165fbce99bb1efa8e026e1ad79d2 \
  -o coverage_report.html coverage_report.xml
```

The HTML version of the xUnit report linked above was then generated using
the third-party converter [xunit-to-html](https://github.com/Zir0-93/xunit-to-html)
with the following commands:

```bash
$ cd xunit-to-html-master
$ java -jar saxon9he.jar \
  -o:$HOME/logtalk/library/dictionaries/xunit_report.html \
  -s:$HOME/logtalk/library/dictionaries/xunit_report.xml \
  -xsl:xunit_to_html.xsl
```

These commands can be easily automated in CI/CD contexts. For automation
examples see e.g. the available Logtalk
[GitHub actions and workflows](https://github.com/logtalk-actions).
