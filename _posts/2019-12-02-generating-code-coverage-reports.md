---
layout: article
title: Generating code coverage reports
tags:
  - best practices
  - testing
show_edit_on_github: false
aside: false
---

You wrote a set of tests for your project and all pass. Time to celebrate?
Well, depends. How good is your tests code coverage? Are all predicates being
called? Are all predicate clauses being tried? How do you know? If you answer
is akin to "by visual inspection", you may be in trouble. Will you be able to
keep up with code changes over time? You may fail to notice code that is not
being exercised. What if tests are assigned to other team member or inherited
by you from others? Code coverage reports should be a standard output when
automating running your tests.

The Logtalk [`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html) tool
supports code coverage stats and reports at the entity predicate clause level.
Nothing like an example to illustrate what we mean:

[Code coverage report for the `diagrams` tool](https://logtalk.org/diagrams/coverage_report.html)

The report provides us with a list of all tested entities and their predicates,
detailing which clauses were used by the tests. It also links to the source
code repository files and lines for easy navigation, simplifying e.g. checking
those clauses that are not being used.

How do we generate these code coverage reports? In our test objects, we must
declare the entities that should be covered using the `cover/1` predicate. For
example, the [`tests`](https://github.com/LogtalkDotOrg/logtalk3/blob/05322cdd799c0dd3c507c91617aaa10eaa0a1f77/tools/diagrams/tests.lgt#L31)
object for the `diagrams` tool contains:

```logtalk
cover(diagram(_)).
cover(diagrams(_)).
cover(entity_diagram(_)).
...
```

We also need to compile the source code in debug mode so that the code coverage
data can be collected when the tests are run (the `lgtunit` tool uses the 
[`logtalk::trace_event/2`](https://logtalk.org/library/logtalk_0.html#trace-event-2)
hook predicate that is part of the debugging API to collect the data). The
[`source_data`](https://logtalk.org/manuals/userman/programming.html#flag-source-data)
flag also needs to be turned on. The flags are usually set in the
[`tester.lgt`](https://github.com/LogtalkDotOrg/logtalk3/blob/05322cdd799c0dd3c507c91617aaa10eaa0a1f77/tools/diagrams/tester.lgt) file that is used to setup and run the tests:

    ...,
    logtalk_load([
        diagram,
        entity_diagram,
        ...
        ], [
        source_data(on), debug(on)
    ]),
    ...

Running the test manually, will print the code coverage data after the tests
results:

```text
| ?- {diagrams(tester)}.
...
% 186 tests: 0 skipped, 186 passed, 0 failed
% completed tests from object tests
% 
% 
% clause coverage ratio and covered clauses per entity predicate
% 
% graph_language_registry: language_object/2 - 0/0 - (all)
% graph_language_registry: 0 out of 0 clauses covered, 100.000000% coverage
% 
% modules_diagram_support: loaded_file_property/2 - 1/1 - (all)
% modules_diagram_support: module_property/2 - 1/1 - (all)
% modules_diagram_support: property_module/2 - 2/7 - [5,6]
% modules_diagram_support: property_source_file/2 - 5/5 - (all)
% modules_diagram_support: source_file_extension/1 - 0/2 - []
% modules_diagram_support: 9 out of 16 clauses covered, 56.250000% coverage
% 
% diagram(A): logtalk::message_tokens//2 - 1/1 - (all)
% diagram(A): logtalk::message_prefix_stream/4 - 0/1 - []
% diagram(A): add_extension/4 - 2/2 - (all)
% diagram(A): add_link_options/3 - 2/2 - (all)
...
```

But how do we generate a nice HTML report as linked above? First, we use
the [`logtalk_tester`](https://logtalk.org/man/logtalk_tester.html)
automation script to generate a code coverage report in XML format:

```bash
$ cd logtalk/tools/diagrams
$ logtalk_tester -c xml
```

Next, we convert the XML report to HTML:

```bash
$ xsltproc \
    --stringparam prefix logtalk/
    --stringparam url https://github.com/LogtalkDotOrg/logtalk3/tree/05322cdd799c0dd3c507c91617aaa10eaa0a1f77/
    -o coverage_report.html coverage_report.xml
```

These steps can be easily automated. Note that we use a permanent link to
a commit using its SHA1 checksum. This ensures that the URLs in the HTML
report to source files and lines remain valid when new commits are pushed.
The final step is to upload the HTML report to an HTTP server (the report
is self-contained using inline CSS). 

### Resources

For more details on `lgtunit` tool support for code coverage reports, consult
its [documentation](https://logtalk.org/manuals/devtools/lgtunit.html).

For an example of CI/CD automation that includes generating and publishing
test and code coverage reports, see e.g. this [`demo`](https://github.com/logtalk-actions/demo)
repo.
