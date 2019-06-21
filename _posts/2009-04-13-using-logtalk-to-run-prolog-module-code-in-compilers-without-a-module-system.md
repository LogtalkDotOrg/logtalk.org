---
title: Using Logtalk to run Prolog module code in compilers without a module system
author: Paulo Moura
layout: article
tags:
  - modules
  - portability
show_edit_on_github: false
aside: false
---

Logtalk can compile most Prolog modules as objects. This is accomplished by recognizing and parsing a common subset of Prolog module directives. For simple module code, it suffices to change the file name extensions from `.pl` to `.lgt` and compile the files as usual using the `logtalk_load/1-2` built-in predicates. For modules that use proprietary predicates, directives, and syntax, some changes to the original code may be necessary.

As an example, assume that we want to use the SWI-Prolog modules `lists`, `pairs`, `oset`, and `ordsets` in GNU Prolog, a compiler that doesn't support a module system. After making a copy of the original files and renaming their extensions to `.lgt`, we will need to remove a few specific, proprietary SWI-Prolog bits. First, we need to comment out all occurrences of the directive:

```logtalk
:- set_prolog_flag(generate_debug_info, false).
```

Second, we need to comment out in `lists.lgt` the calls to the `must_be/2` predicate and the line:

```logtalk
:- use_module(error, [must_be/2]).
```

Still in `lists.lgt` we will need to replace the call to the `succ/2` by:

```logtalk
M is N + 1,
```

Third, Logtalk doesn't support the `use_module/1` directive, requiring instead the use of the `use_module/2` directive. Thus, we need to replace the directive:

```logtalk
:- use_module(library(oset)).
```

with the directive:

```logtalk
:- use_module(oset,
        [oset_int/3, oset_addel/3, oset_delel/3,
         oset_diff/3, oset_union/3]).
```

Finally, `is_list/1` is a built-in predicate in SWI-Prolog but not in GNU Prolog. Logtalk provides its own portable versions of the `is_list/1`, `succ/2`, and `must_be/2` predicates but let's leave them out for now, for the sake of simplicity. After saving our changes, we are ready for a quick experiment:

```text
$ gplgt
...
Logtalk 2.36.0
Copyright (c) 1998-2009 Paulo Moura
...
GNU Prolog 1.3.1
By Daniel Diaz
Copyright (C) 1999-2009 Daniel Diaz
| ?- {lists, pairs, oset, ordsets}.
...
yes
| ?- pairs::map_list_to_pairs(lists::length,[[1,2],[a,b,c],[X]],Pairs).

Pairs = [2-[1,2],3-[a,b,c],1-[X]]
yes
```

In SWI-Prolog the equivalent call would be:

```text
$ swipl
...
Welcome to SWI-Prolog (Multi-threaded, 32 bits, Version 5.7.8)
...
?- pairs:map_list_to_pairs(length,[[1,2],[a,b,c],[X]],Pairs).
Pairs = [2-[1, 2], 3-[a, b, c], 1-[X]].
```

So, all done? Not quite. Different Prolog compilers provide different sets of built-in predicates. Module libraries use those built-in predicates. Thus, porting module code must also check for used built-in predicates. Fortunately, that's quite easy in Logtalk: we simply compile the files with the `portability` compiler flag set to `warning`. In the case of our example, there is no problem for GNU Prolog but if we try to load our files in e.g. B-Prolog (another compiler without a module system) we will find that the `lists` module calls a `memberchk/2` predicate that is not built-in in this compiler.

The porting process is not as straightforward as we may hoped for, but nothing is really straightforward when dealing with Prolog portability issues. The code changes needed are usually simple to apply as the example above illustrates. A small price to pay when porting module code. I'm sure you appreciate the irony of using Logtalk to run Prolog module code in module-less Prolog compilers. The subset of module directives recognized by Logtalk is enough for dealing with most Prolog module libraries. This subset could also provide a basis for a Prolog module standard based on current practice but that's a topic for another post.

P.S. The predicate `succ/2` is defined in the Logtalk library object `integer`. An equivalent predicate to `is_list/1` is defined in the Logtalk library object `list`, which also defines a `memberchk/2` predicate. Moreover, each Logtalk library object that defines a _type_ contains a definition for a `check/1` predicate that plays the same role as the SWI-Prolog library predicate `must_be/2`.
