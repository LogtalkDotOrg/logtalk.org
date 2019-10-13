---
layout: article
permalink: using_tools_with_prolog.html
title: Using Logtalk tools with Prolog codebases
aside:
  toc: true
---

With some limitations, it's possible to use several of the Logtalk developer
tools with Prolog codebases. In doing so, keep in mind that Logtalk (1) uses
Prolog as a backend compiler and (2) is designed to be Prolog agnostic. The
lack of sensible standardization, particularly of modules and term-expansion
mechanisms, means that each Prolog system provides its own proprietary
implementation of these and other concepts and mechanisms, precluding portable
solutions. The Prolog adapter files used by Logtalk contain code to workaround
some of these portability issues.

For best results, always use the latest Logtalk version to benefit of any
recent improvements to the Logtalk compiler and Prolog backend adapter files
that facilitate compiling Prolog code as Logtalk code.

This guide is most relevant for using Logtalk's [`linter`](tools.html#lint-checker),
[`dead_code_scanner`](tools.html#dead-code-scanner), [`code_metrics`](tools.html#code-metrics),
and [`ports_profiler`](tools.html#ports-profiler) tools to analyze and debug
issues in Prolog code. Other tools, such as [`lgtunit`](tools.html#testing),
directly support Prolog code.

**Note:** If you're instead considering porting a Prolog application to Logtalk,
there's a tool, [`wrapper`](tools.html#prolog-porting) that can help. In that
case, this is not the guide you're looking for.

### Plain Prolog code

Applying the Logtalk developer tools to plain Prolog code (i.e. Prolog code
not encapsulated in modules) requires wrapping the code using Logtalk objects.
A simply way of doing it is creating a Logtalk source file per Prolog source
file, defining an object that uses an `include/1` directive to load the
Prolog code. For example, assuming a `foo.pl` file, we can create a `foo.lgt`
file defining the object:

	:- object(foo).
	
	    :- include('foo.pl').
	
	:- end_object.

Keep in mind that some Prolog directives are not valid inside objects and
can cause compilation errors. If that's the case, is best to make a copy
of the Prolog files and edit them to add the object wrapper and either
move the directives to outside the object or comment them.


### Prolog modules

The Logtalk compiler supports compiling modules (that only make use of a
common subset of directives) as objects. As, in general, a Prolog source
file defines a single module, we can simply compile the Prolog files
as Logtalk files. This doesn't require any file extension changes but just
passing the names of the files to the Logtalk compilation and loading
built-in predicates.

Start by loading the Prolog modules as usual (modules and objects live
in different namespaces, which avoids most conflicts). This first step
allows Logtalk to query the runtime about module exported predicates.
For example, if you use a `loader.pl` file to load your application:

	| ?- [loader].
	...

Next, try to compile the Prolog source files as Logtalk source files. For
example, assuming a directory with Prolog files using the common `.pl`
extension and a Prolog system providing the de facto standard `forall/2`
and `member/2` predicates:

	| ?- {os(loader)}.
	...
	
	| ?- os::directory_files('.', Files, [type(regular),extensions(['.pl']),paths(relative)]),
	     forall(member(File,Files), (logtalk_load(File) -> true; true)).
	...

The Logtalk compiler linter will run automatically (but note that some checks
may be turned off by default; if so, use the `set_logtalk_flag/2` predicate to
turn them on). Other tools will need to be loaded and applied to the loaded
files (see the tools documentation for details).

**Note:** As the `logtalk_load/1` predicate fails on the first compilation error,
we use the if-then-else control construct in the query above to advance to the
next file in case of error. Those errors are usually caused by Prolog proprietary
extensions. How to workaround some of those errors is discussed next.

### Prolog code using a term-expansion mechanism

Some Prolog systems and their typical applications may make use of a
term-expansion mechanism. When the Prolog system implements these mechanism
using `term_expansion/2` and `goal_expansion` predicates with clauses for
them collected in a selected number of modules, it's possible to instruct
Logtalk own term-expansion mechanism to call the Prolog defined expansions.
For example, assume that the used Prolog libraries and user modules
defining expansions store them in the `user` and `system` modules. In this
case, before attempting to compile the Prolog code as Logtalk objects, try
the following queries:

	| ?- {hook_flows(loader)}.
	...

	| ?- set_logtalk_flag(hook, hook_set([user,system])).
	...

### File loading order

Most Prolog applications load their files in a specific order. For example,
when user-defined operators are used, the file defining those operators is
loaded first. Some Prolog applications use an explicit loader file. For
best results when trying to use the Logtalk developer tools, take into
account the loading order. If necessary, write a simple `loader.lgt` file
instead of using the `forall/2` loop illustrated above.

### Know issues

When finding a `use_module/1` or `use_module/2` directive in a Prolog module,
Logtalk either successfully expands it to a Logtalk supported `use_module/2`
directive (which takes as first argument a module name instead of a file
specification) or prints an error and aborts the compilation of the source
file. If you get an error, load the module file first and try again. Note
that the expansion from a Prolog `use_module/1` directive to a Logtalk
`use_module/2` directive will likely result in false positives when using
the `dead_code_scanner` tool.

The `set_prolog_flag/2` directive cannot be used inside objects but is
sometimes used inside modules. The workaround is to move those directives
to outside the modules before attempting to compile the modules as objects.
