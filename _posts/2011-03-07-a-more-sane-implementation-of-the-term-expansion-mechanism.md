---
title: A more sane implementation of the term-expansion mechanism
author: Paulo Moura
layout: article
tags:
  - term-expansion
  - portability
  - best practices
show_edit_on_github: false
aside: false
---

One of the oldest and more useful feature found in most Prolog compilers is the term-expansion mechanism. Acting as a souped-up pre-processor, defining term- and goal expansion clauses allows us to rewrite terms and goals as their are read from a source file and apply all kinds of transformations. This made term-expansion the preferred mechanism for implementing all sorts of extensions to Prolog.

You may be wondering if the Logtalk compiler is also implemented using the term-expansion mechanism. The answer is no. One of the main reasons is that the term-expansion mechanism is not implemented by all Prolog compilers. Among those that do implement term-expansion, there are also some minor (and not so minor) syntax and semantics differences. The real trouble with term-expansion results, however, from its usual implementation and usage patterns, combined with module features, not from those portability issues.

The usual pattern when implementing some Prolog extension using the term-expansion mechanism is to define a module, relying on term- and goal-expansion clauses to compile to standard Prolog code the syntactic elements defined by the extension. As the recommended way of using modules is to simply use a `use_module/1` directive to make the module resources available in your current context (how convenient and easy is to shoot yourself in the foot&#8230; but I digress), the `term_expansion/2` and `goal_expansion/2` predicates are declared as multifile predicates, with the clauses ending up either on the `user` module or on a special system module. Either way is fine until you try to use more than one module that defines `term_expansion/2` clauses. The Prolog compiler will try `term_expansion/2` clauses until it finds one that succeeds for the term being expanded or until there are no more clauses left to try (the `goal_expansion/2` predicate, however, is called recursively until no more goal-expansion clauses apply). Assuming that no two Prolog modules want to expand the same term (one can always hope), there should no problem. Sure, there might be a performance issue due to trying and failing `term_expansion/2` clauses until the correct one is selected. But what happens if two modules compete for expanding the same term? Say, the `end_of_file` term. Well, if the module developers are not aware of the problem, one of them will likely lose. Each one? That will depend on the modules loading order. The usual workaround is to define `term_expansion/2` clauses that perform their magic using side-effects to record the results and fail when done. The failure leads to backtracking, giving other `term_expansion/2` clauses a chance to be applied. Ugliness of using side-effects apart, there is a more sane way of implementing and using the term-expansion mechanism.

One of the advantages of not being first (to design and try a new mechanism) is that you can learn from both the successes and mistakes of others before you. You also have a significant advantage by not having to care about breaking backward compatibility. The implementation of term-expansion in Logtalk differs from the implementation found on most Prolog compilers in two crucial aspects.

First, Logtalk doesn't support using the term- and goal expansion clauses defined in an object (or source file) to expand the object (or source file) itself. It's already bad enough that some predicate directives must precede the compilation of calls to those predicates. But having the result of the compilation of an object (or source file) depend on the order of the predicate definitions in the same object (or source file) feels plain wrong. Specially as it's an exception to the way both Logtalk and Prolog compilers work. Just imagine being forced to define all predicates called by a predicate before it could be defined. It will be painful. It would also be impossible in some cases. Yet, well know Prolog extensions do just that, throwing portability down the drain (not all Prolog compilers make predicate definitions visible and usable, as soon as they are compiled, without waiting for the rest of the source file to be compiled&#8230;).

Second, term- and goal-expansion clauses are defined local to the object where they are defined. It's possible to add those clauses to the pseudo-object `user` (Logtalk supports multifile object predicates). But that is neither necessary or advised. Do we really want to put all our eggs&#8230; err&#8230; term-expansion hooks in the same basket?

So, what's the magic incantation to use term-expansion in Logtalk? Easy. Objects containing clauses for the term- and goal expansion predicates are known as hook objects. When compiling a source file, you use a compiler option to state which hook object should be used to term-expand the source file. For example, assuming a hook object named `my_expansion` we could write:

```text
| ?- logtalk_load(source_file, [hook(my_expansion)]).
```

This compiler option also provides a nice solution for combining different hook objects in order to expand the same source file. You simply define another hook object that calls the term- and goal-expansion predicates defined in the base hook objects. This allows fine control on how the different expansions will work together. For example, we can define a pipeline of goal-expansions. Or apply all term-expansions in parallel and combine the resulting terms. For some sample code, check the `expanding` example in the current Logtalk distribution. Or browse the example source code on-line:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/expansion](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/expansion)

Even when a source file is to be expanded using a single hook object, we can be ensured that the compilation time will not be adversely affected by other hook objects that might be loaded at the time of the compilation. The code also becomes easier to debug as only the relevant term-expansion clauses will be in focus.

P.S. It's worth noting that the Logtalk term-expansion implementation and recommended usage patterns can be easily adopted by Prolog module systems. In that regard, it's also worth noting that some Prolog compilers, e.g. SICStus Prolog and Ciao Prolog, already include improved implementations of term-expansion mechanisms.
