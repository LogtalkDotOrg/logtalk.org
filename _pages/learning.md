---
layout: article
permalink: learning.html
title: Learning by examples
aside:
  toc: true
---

Logtalk is a programming language that extends and subsumes Prolog. Thus, a good knowledge of Prolog paves the way for a quick learning of Logtalk programming. Basic knowledge of object-oriented programming also helps, specially if from a generalized, first principles, approach. It is highly recommended that you start with the tutorial available at:

[Learn X in Y minutes Where X=Logtalk](https://learnxinyminutes.com/docs/logtalk/)

Note that the Logtalk distribution includes both HTML versions of the user
manual, the reference manual, and the APIs documentation. It can also be
browsed at:

[Logtalk documentation resources](documentation.html)

The Logtalk distribution also includes a large number of well documented
programming examples that introduce most of the language features. The
examples included are fully documented with source code comments and sample
goals:

[Programming examples](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples)
(described [here](https://github.com/LogtalkDotOrg/logtalk3/blob/master/examples/NOTES.md)).

All examples include a `loader.lgt` file that loads the example and any dependencies, a `NOTES.md` file with a description of the example, and a `SCRIPT.txt` file with sample queries (including how to load the example) for you to try. Most examples also include a `tests.lgt` file with unit tests and a `tester.lgt` loader file to run them. Being programming examples, it is expected that you run them side-by-side with the source code open in your [favorite editor](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding).

[Learning and development tools](tools.html)

To help new users understand and act on compiler and runtime warning and error messages, load the [`tutor`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/tutor/NOTES.md) tool at startup.
To help new users trace query execution, also load the [`debugger`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/debugger/NOTES.md) tool at startup.
These and other developer tools (e.g. for testing and documentation) can be automatically loaded
at startup by defining a default
[settings file](https://github.com/LogtalkDotOrg/logtalk3/tree/master/settings-sample.lgt).

## Examples recommended walkthrough

* [`hello_world`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/hello_world) - mandatory example; cannot be avoided
* [`roles`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/roles) - learn about the different roles that an object can play
* [`scopes`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/scopes) - learn about predicate scopes
* [`self_messages`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/self_messages) - learn how to use messages to *self* to call redefined predicates
* [`super_calls`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/super_calls) - learn how to use *super* calls to specialize inherited predicates
* [`elephants`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/elephants) - learn about the concept of prototypes
* [`prototypes`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/prototypes) - another example on prototypes
* [`planets`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/planets) - learn how to define and use protocols and categories
* [`carengines`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/carengines) - learn more about categories
* [`shapes`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/shapes) - learn about the differences between class and prototype hierarchies
* [`inheritance`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/inheritance) - learn more about inheritance
* [`family`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/family) - no self respecting logic programming language can do without a family relations example

Need a break after playing with the above examples? Have fun with the following ones:

* [`adventure`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/adventure) - text-based adventure games; beware of the monsters!
* [`puzzles`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/puzzles) - logical puzzles

The Logtalk compiler does extended lint checks. Trouble understanding compiler output? Want to learn more about compilation errors and warnings? There's an example for that:

* [`errors`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/errors) - learn about compiler errors and warnings

Want to learn about parametric objects (and categories)? See the following examples:

* [`parametric`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/parametric)
* [`parvars`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/parvars)
* [`proxies`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/proxies)
* [`symdiff`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/symdiff)

Logtalk support for _composition_ using categories provides an alternative to _inheritance_. Two good examples are:

* [`points`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/points)
* [`polygons`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/polygons)

Another distinctive Logtalk feature is the support for _event-driven programing_. Some illustrative examples are:

* [`profiling`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/profiling)
* [`blocks`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/blocks)

Looking for how to express traditional OOP class concepts from other languages in Logtalk? See:

* [`people`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/people)
* [`metaclasses`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/metaclasses)
* [`reflection`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/reflection)
* [`roots`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/roots)
* [`classmethods`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/classmethods)
* [`classvars`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/classvars)
* [`instmethods`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/instmethods)
* [`instvars`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/instvars)

Now that you got the basics of OOP in Logtalk, time to take it to the next level:

* [`design_patterns`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/design_patterns)

But Logtalk is a _declarative_ language supporting all those features that drive people to logic programming. Some good examples are:

* [`dcgs`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/dcgs)
* [`metainterpreters`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/metainterpreters)
* [`metapredicates`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/metapredicates)
* [`lambdas`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/lambdas)
* [`searching`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/searching)
* [`coinduction`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/coinduction)
* [`constraints`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/constraints)
* [`engines`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/engines)
* [`tabling`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/tabling)

Looking for extending Logtalk with your constructs? Logtalk supports a term-expansion mechanism (aka as macros):

* [`hooks`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/hooks)
* [`wrappers`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/wrappers)

Happy about your progress? Time to celebrate with:

* [`bottles`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/bottles) - sing along!

## Running example queries in the debugger

Running a query using the debugger can help understand the inference process.
An example session, using the [`planets`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/planets) example:

```
?- {planets(loader)}.
% [ /Users/pmoura/logtalk/examples/planets/planets.lgt loaded ]
% [ /Users/pmoura/logtalk/examples/planets/loader.lgt loaded ]
% (0 warnings)
true.
```
In the context of the top-level interpreter, the `{}/1` goal is just a handy shortcut for
the [`logtalk_load/1`](https://logtalk.org/manuals/refman/predicates/logtalk_load_1.html)
predicate. The argument uses _library notation_ to specify the file to load: `planets` is
the library name (an alias to a directory of source files) and `loader` is the
file name (with the extension omitted).

Let's try a query:

```
?- mars::weight(m2, W2).
W2 = 14.88304.
```

How do Logtalk arrived to this solution? Let's recompile the example in _debug_ mode:

```
?- {+d}.
% Reloading files in debug mode
% Redefining protocol physical_properties
% Redefining category planet
% Redefining object m1
% Redefining object m2
% Redefining object earth
% Redefining object mars
% [ /Users/pmoura/logtalk/examples/planets/planets.lgt reloaded ]
% [ /Users/pmoura/logtalk/examples/planets/loader.lgt reloaded ]
% (0 warnings)
% Reloaded all Logtalk source files modified or that required
% recompilation due to a change to the compilation mode
true.
```

The `{+d}` goal is a top-level shortcut for the [`logtalk_make/1`](https://logtalk.org/manuals/refman/predicates/logtalk_make_1.html)
predicate that recompiles loaded files in debug mode.

We also need to load the debugger (hint: you can load the debugger and other tools automatically at startup by defining a default [settings file](https://github.com/LogtalkDotOrg/logtalk3/tree/master/settings-sample.lgt)):

```
?- {debugger(loader)}.
% [ /Users/pmoura/logtalk/tools/debugger/debuggerp.lgt loaded ]
% [ /Users/pmoura/logtalk/tools/debugger/debugger.lgt loaded ]
% [ /Users/pmoura/logtalk/tools/debugger/debugger_messages.lgt loaded ]
% [ /Users/pmoura/logtalk/tools/debugger/loader.lgt loaded ]
% (0 warnings)
true.
```
We can now trace the query:

```
?- debugger::trace.
   Debugger switched on: tracing everything for all objects compiled in debug mode.
true.

?-  mars::weight(m2, W2).
   Call: (1) weight(m2,_1228) ? 
   Rule: (1) weight(m2,_1228) ? x
     Entity:            planet
     Sender:            user
     This:              mars
     Self:              mars
     Meta-call context: []
     Coinduction stack: []
   Rule: (1) weight(m2,_1228) ? 
   Call: (2) m2::mass(_2348) ? 
   Call: (3) mass(_2348) ? 
   Fact: (3) mass(4) ? 
   Exit: (3) mass(4) ? 
   Exit: (2) m2::mass(4) ? 
   Call: (4) ::gravitational_acceleration(_4622) ? 
   Call: (5) gravitational_acceleration(_4622) ? 
   Fact: (5) gravitational_acceleration(3.72076) ? x
     Entity:            mars
     Sender:            mars
     This:              mars
     Self:              mars
     Meta-call context: []
     Coinduction stack: []
   Fact: (5) gravitational_acceleration(3.72076) ? 
   Exit: (5) gravitational_acceleration(3.72076) ? 
   Exit: (4) ::gravitational_acceleration(3.72076) ? 
   Call: (6) _22 is 4*3.72076 ? 
   Exit: (6) 14.88304 is 4*3.72076 ? 
   Exit: (1) weight(m2,14.88304) ? 
W2 = 14.88304.
```

The debugger supports a several handy options. Type `h` or `?` at its prompt for inline help. Consult the user manual section on [debugging](https://logtalk.org/manuals/userman/debugging.html) for further information.

To terminate the debugging session, you can turn off the debugger and recompile the files in normal (or optimized mode):

```
?- debugger::nodebug.
   Debugger switched off.
true.

?- {+n}.
% Reloading files in normal mode
% Redefining protocol physical_properties
% Redefining category planet
% Redefining object m1
% Redefining object m2
% Redefining object earth
% Redefining object mars
% [ /Users/pmoura/logtalk/examples/planets/planets.lgt reloaded ]
% [ /Users/pmoura/logtalk/examples/planets/loader.lgt reloaded ]
% (0 warnings)
% Reloaded all Logtalk source files modified or that required
% recompilation due to a change to the compilation mode
true.
```

## Modifying and reloading an example

But don't just run the provided examples. Experiment also modifying them. Continuing to use the `planets` example, let's add another planet, `jupiter`, by editing the `planets.lgt` file. At the end of the file, we can write:

```logtalk
:- object(jupiter,
    imports(planet)).

    gravitational_acceleration(25.885).

:- end_object.
```

As we just modified a loaded file, we can use the [`make`]((https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/make/NOTES.md)) tool to reload it:

```
?- {*}.
% Redefining protocol physical_properties
% Redefining category planet
% Redefining object m1
% Redefining object m2
% Redefining object earth
% Redefining object mars
% [ /Users/pmoura/logtalk/examples/planets/planets.lgt reloaded ]
% (0 warnings)
% Reloaded all Logtalk source files modified or that required
% recompilation due to a change to the compilation mode
true.

?- jupiter::weight(m2, W2).
W2 = 103.54.
```

The `{*}` goal is a top-level shortcut to the `logtalk_make` goal (and the `logtalk_make(all)` goal).

## Running example tests

Next we could also modify the example unit tests to account for the newly added `jupiter` object by editing the `tests.lgt` file. As we added a new object, `jupiter`, we want to add a `cover/1` clause for it to that we can collect cove coverage data:

```logtalk
cover(jupiter).
```

After saving the changes to the `tests.lgt` file, we can run the tests by simply loading the `tester.lgt` file:

```
?- {planets(tester)}.
% 
% tests started at 2019/2/20, 14:34:43
% 
% running tests from object tests
% file: /Users/pmoura/logtalk/examples/planets/tests.lgt
% 
% planets_01: success
% planets_02: success
% planets_03: success
% planets_04: success
% 
% 4 tests: 0 skipped, 4 passed, 0 failed
% completed tests from object tests
%
% 
% clause coverage ratio and covered clauses per entity predicate
% 
% earth: gravitational_acceleration/1 - 1/1 - (all)
% earth: 1 out of 1 clause covered, 100.000000% coverage
% 
% jupiter: gravitational_acceleration/1 - 0/1 - []
% jupiter: 0 out of 1 clause covered, 0.000000% coverage
% 
% m1: mass/1 - 1/1 - (all)
% m1: volume/1 - 0/1 - []
% m1: 1 out of 2 clauses covered, 50.000000% coverage
% 
% m2: mass/1 - 1/1 - (all)
% m2: volume/1 - 0/1 - []
% m2: 1 out of 2 clauses covered, 50.000000% coverage
% 
% mars: gravitational_acceleration/1 - 1/1 - (all)
% mars: 1 out of 1 clause covered, 100.000000% coverage
% 
% planet: weight/2 - 1/1 - (all)
% planet: gravitational_acceleration/1 - 0/0 - (all)
% planet: 1 out of 1 clause covered, 100.000000% coverage
% 
% 6 entities declared as covered containing 8 clauses
% 5 out of 6 entities covered, 83.333333% entity coverage
% 5 out of 8 clauses covered, 62.500000% clause coverage
% 
% tests ended at 2019/12/13, 14:29:25
% 
true.
```

As expected, there is no code coverage for the new `jupiter` object. To fix it, we can take the query we used above and add it as a test:

```logtalk
test(planets_05) :-
    jupiter::weight(m2, W2),
    W2 =~= 103.54.
```

Consult the documentation of the [`lgtunit`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md) testing tool to learn more about testing, including more expressive test dialects. 

At this point, you should have a good understanding of the basics of Logtalk programming. But there are more features to explore and many more examples for you to play with. We suggest that you look into the [examples summary](https://github.com/LogtalkDotOrg/logtalk3/blob/master/examples/NOTES.md) and choose the next ones according to your interests.

Enjoy and remember: the [discussion forums](http://forums.logtalk.org/) and the [chat room](https://gitter.im/LogtalkDotOrg/logtalk3) welcome your participation. Don't be a stranger. 