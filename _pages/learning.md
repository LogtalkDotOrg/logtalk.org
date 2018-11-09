---
layout: article
permalink: learning.html
title: Learning
aside:
  toc: true
---

Logtalk is a programming language that extends and subsumes Prolog. Thus, a good knowledge of Prolog paves the way for a quick learning of Logtalk programming. Basic knowledge of object-oriented programming also helps, specially if from a generalized, first principles, approach. It is highly recommended that you start with the tutorial available at:

[Learn X in Y minutes Where X=Logtalk](https://learnxinyminutes.com/docs/logtalk/)

Note that the Logtalk distribution includes both HTML versions of the user manual, the reference manual, and the APIs documentation. It can also be browsed at:

[Logtalk documentation resources](documentation.html)

The Logtalk distribution also includes a large number of well documented programming examples that introduce most of the language features.
The examples included are fully documented with source code comments and sample goals:

[Programming examples](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples)
(described [here](https://github.com/LogtalkDotOrg/logtalk3/blob/master/examples/NOTES.md)).

All examples include a `NOTES.md` file with a description and a `SCRIPT.txt` file with sample queries for you to try. Being programming examples, it is expected that you run them side-by-side with the source code open in your [favorite editor](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding). Follows a suggested order for playing with the examples:

## Examples recommended walkthrough

* `hello_world` - mandatory example; can't be avoided
* `roles` - learn about the different roles that an object can play
* `scopes` - learn about predicate scopes
* `self_messages` - learn how to use messages to self to call redefined predicates
* `super_calls` - learn how to use super calls to specialize inherited predicates
* `elephants` - learn about the concept of prototypes
* `prototypes` - another example on prototypes
* `planets` - learn how to define and use protocols and categories
* `carengines` - learn more about categories
* `shapes` - learn about the differences between class and prototype hierarchies
* `inheritance` - learn more about inheritance
* `family` - no self respecting logic programming example can do without a family relations example

Next a break after playing with the above examples? Have fun with the following ones:

* `adventure` - text-based adventure games; beware of the monsters!
* `puzzles` - logical puzzles

The Logtalk compiler does extended lint checks. Trouble understanding compiler output? Want to learn more about compilation errors and warnings? There's an example for that:

* `errors` - learn about compiler errors and warnings

Want to learn about parametric objects (and categories)? See the following examples:

* `parametric`
* `parvars`
* `proxies`
* `symdiff`

Logtalk support for _composition_ using categories provides an alternative to _inheritance_. Two good examples are:

* `points`
* `polygons`

Another distinctive Logtalk feature is the support for _event-driven programing_. Some illustrative examples are:

* `profiling`
* `blocks`

Looking for how to express traditional OOP class concepts from other languages in Logtalk? See:

* `roots`
* `metaclasses`
* `classmethods`
* `classvars`
* `instmethods`
* `instvars`
* `people`

But Logtalk is a _declarative_ language supporting all those features that drive people to logic programming. Some good examples are:

* `dcgs`
* `metainterpreters`
* `metapredicates`
* `lambdas`
* `searching`
* `coinduction`
* `constraints`
* `engines`
* `tabling`

Looking for extending Logtalk with your constructs? Logtalk supports a term-expansion mechanism (aka as macros):

* `hooks`
* `wrappers`

Happy about your progress? Time to celebrate with:

* `bottles` - sing along!

## Running example queries in the debugger

Running a query using the debugger can help understand the inference process. An example session, using the `planets` example:

```
?- {planets(loader)}.
% [ /Users/pmoura/logtalk/examples/planets/planets.lgt loaded ]
% [ /Users/pmoura/logtalk/examples/planets/loader.lgt loaded ]
% (0 warnings)
true.
```
The `{}/1` goal is just a handy top-level shortcut for the
[`logtalk_load/1`](https://logtalk.org/manuals/refman/predicates/logtalk_load_1.html)
predicate. Let's try a query:

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

?- mars::weight(m2, W2).
   Call: (7) weight(m2,_994) ? 
   Rule: (7) weight(m2,_994) ? x
     Entity:            planet
     Sender:            user
     This:              mars
     Self:              mars
     Meta-call context: []
     Coinduction stack: []
   Rule: (7) weight(m2,_994) ? 
   Call: (8) m2::mass(_2040) ? 
   Call: (9) mass(_2040) ? 
   Fact: (9) mass(4) ? 
   Exit: (9) mass(4) ? 
   Exit: (8) m2::mass(4) ? 
   Call: (10) ::gravitational_acceleration(_4208) ? 
   Call: (11) gravitational_acceleration(_4208) ? 
   Fact: (11) gravitational_acceleration(3.72076) ? x
     Entity:            mars
     Sender:            mars
     This:              mars
     Self:              mars
     Meta-call context: []
     Coinduction stack: []
   Fact: (11) gravitational_acceleration(3.72076) ? 
   Exit: (11) gravitational_acceleration(3.72076) ? 
   Exit: (10) ::gravitational_acceleration(3.72076) ? 
   Call: (12) _994 is 4*3.72076 ? 
   Exit: (12) 14.88304 is 4*3.72076 ? 
   Exit: (7) weight(m2,14.88304) ? 
W2 = 14.88304.
```

The debugger supports a several handy options. Type `h` or `?` at its prompt for inline help. Consult the  [user manual](https://logtalk.org/manuals/userman/index.html) for further information.

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

At this point, you should have a good understanding of the basics of Logtalk programming. But there are more features to explore and many more examples for you to play with. We suggest that you look into the [examples summary](https://github.com/LogtalkDotOrg/logtalk3/blob/master/examples/NOTES.md) and choose the next ones according to your interests.

Enjoy and remember: the [Logtalk discussion forums](http://forums.logtalk.org/) and the [Logtalk chat room](https://gitter.im/LogtalkDotOrg/logtalk3) are at your disposable. Don't be a stranger. 