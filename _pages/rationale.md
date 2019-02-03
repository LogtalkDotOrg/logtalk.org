---
layout: article
permalink: rationale.html
title: Rationale
aside:
  toc: true
---

## Why Logtalk?

Logtalk is designed to _extend_ and _leverage_ Prolog. It provides an alternative for Prolog modules, subsuming their functionality, complemented with a comprehensive set of [developer tools](tools.html). By Prolog modules we assume here the de facto standard module system introduced by Quintus Prolog and adapted by most of the Prolog systems that provide an implementation of modules. Although Prolog systems adapted the original module system introducing several proprietary variations (and consequent severe portability issues), the fundamental characteristics remain:

* Designed as a simple solution to to hide auxiliary predicates
* Based on a _predicate prefixing_ mechanism
* Reuse based on _import/export_ semantics
* Strongly biased towards implicit predicate qualification

These fundamental characteristics make module systems relatively simple to implement but also effectively prevent extending them to provide several key features present in Logtalk, some of them described here, that support a wide range of code encapsulation and reuse scenarios typically found in applications. Notably, Logtalk enables simple implementations of common design patterns that are cumbersome at best using Prolog modules.

Logtalk also fixes some murky predicate semantics found in Prolog, improves some it its key mechanisms, and provides unique libraries. Note that all advantages described next _coexist_ with Prolog. I.e. Logtalk acts strictly as an _add-on_. It does not patch or modify Prolog own built-in features.

### Protocols (interfaces)

Protocols are first-class entities in Logtalk. Being able to define a protocol (or interface) and provide multiple implementations is one of the most basic features for an encapsulation mechanisms. Protocols are also a key part of most design patterns in software engineering. Its absence in module systems twists practice and leads to non scalable, brittle solutions.

The current and recommended practice with Prolog modules is that *exported* predicates should not clash and to prefer `use_module/1` directives over `use_module/2` directives or explicit module qualification. These recommendations are as convenient (specially for new users) as they are problematic. The first consequence, is that modules, as encapsulation units, are in practice only there to prevent clashes between *private* predicates. But there isn't any central authority for modules. Nor is reasonable to expect or demand that programmers all over the world sync before deciding the names of exported predicates when releasing a public module library. Users may also find that newly released libraries clash with their own modules. The preference for `use_module/1` directives also means that adding a new exported predicate to a module library can cause a module conflict and thus break existing applications that, necessarily, don't use the new predicate. A common symptom (and workaround) for these issues is prefixing exported module predicates with an abbreviation of the module name to prevent clashes (see e.g. the `ordsets`, `random`, or `rbtrees` modules).

Note that separation of interface and implementation for modules, with multiple modules implementing the same interface, is not a question of finding an hypothetical ingenious solution. The semantics of the `:/2` module qualification operator and the `module/2` directive don't provide the necessary distinction between _declaring_ and _defining_ a predicate.

### _Declaring_ a predicate vs _defining_ a predicate

Logtalk provides a clear distinction between _declaring_ and _defining_ a predicate and thus clear closed world assumption semantics. Messages or calls for declared but undefined predicates fail. Messages or calls for unknown (not declared) predicates throw an error. Note that this is a fundamental requirement for protocols/interfaces: we must be able to *declare* a predicate without necessarily *defining* it.

In contrast, in module systems it's either a compiler error to try to export a predicate that is not defined or a predicate existence error to try to call an exported predicate that is not defined. The absence of a protocol/interface concept in module systems is sometimes hacked using `include/1` directives. But that leads to versioning of files instead of versioning of interfaces and does not provide a solution that allows two or more modules to implement the same interface as discussed above.

Note that modules are a _predicate prefixing_ solution and thus any call to a module predicate requires it to be defined in the module that is implicit or explicit in the call (otherwise a predicate existence error is generated). There is no predicate _lookup_ that would allow to verify that a predicate is _declared_ prior to calling it.

### Consistent predicate call semantics

In Logtalk, implicit message sending, using `uses/2` directive to resolve the messages, and explicit message sending, using the `::/2` control construct, have the same semantics for both meta-predicates and non meta-predicates. I.e. using using implicit or explicit messages is simply a matter of programming style and programmer preference. For meta-predicates, this results in clear and clean meta-predicate call semantics: meta-arguments are **always** called in the meta-predicate _calling context_.

Prolog modules, however, provide different semantics for implicit and explicit qualified calls to meta-predicates. Calling a module meta-predicate with implicit qualification (by using `use_module/1-2` directives) results in the meta-arguments being called in the meta-predicate _calling context_. But calling the same module meta-predicate using explicit qualification results in the meta-arguments being called in the meta-predicate _definition context_, not in the _calling context_.

Consistent predicate call semantics require an implicit and comprehensive execution context that is alien to module systems. In Logtalk, this implicit execution context allows the language runtime to be aware of the _calling context_ and thus fully support not only consist predicate call semantics but also key features such as messages to _self_ and _super_ calls (which must preserve _self_ for correct semantics).

### No predicate loading conflicts 

Module predicate import/export semantics and the common (and often recommended) practice of using `use_module/1` directives prevents loading in the same context two modules exporting the same predicate. This means that **any** update that strictly adds new exported predicates to module libraries have the potential to break existing applications. These loading conflicts can only be prevented by using `use_module/2` directives or resorting to explicit qualification.

In contrast, loading two or more objects that declare the same predicate as public does not create any conflicts as Logtalk does not use the concept of predicates importing/exporting found in Prolog modules. This means e.g. that a Logtalk update that strictly adds new public predicates to its libraries cannot break existing applications as implicit message sending is only possible using `uses/2` directives. No equivalent to `use_module/1` directives is provided.

### _Loading_ a file vs _using_ an entity

Logtalk provides a clear separation between loading a file and using an entity. Loading a file does not imply any kind of _using_ relation between existing entities and the entities being loaded. But in Prolog module systems, the `use_module/1-2` directives take as first argument a specification of a file to be loaded and not a module name (which may or may not be the same as the file basename) and both load the file and import the listed predicates (in case of a `use_module/2` directive) or all exported predicates of the module being loaded (in case of a `use_module/1` directive). The `ensure_loaded/1` directive also takes a file specification as argument but, depending on the Prolog system, it either behaves as `use_module/1` directive or as a `use_module/2` directive with an empty list as second argument. The potential problems of the implicit importing of the `use_module/1` directive have already been discussed.

### Predicate names are not owned by objects

The same predicate name can be a public predicate of any number of objects. This means that object interfaces can use the best possible predicate names, simplifying and minimizing protocols vocabulary, making APIs easy to learn. In contrast, current practice with Prolog modules is that exported predicates should never conflict. But this is not scalable and results with different vocabulary being used for otherwise similar module interfaces. As an example, `member/2` is a predicate usually exported by a `lists` module. But `member/2` is also a good name for e.g. modules representing sets or trees. But the emphasis in implicit qualification using `use_module/1` directives effectively prevents using the `member/2` predicate name for anything other than lists.

### Simple scope rules for flags

The `set_logtalk_flag` **directive** is always local to their scope, which can be an entity or a source file. Only calls to the `set_logtalk_flag` **predicate** set the global default value for a flag.

In contrast, some Prolog flags have local scope while others have global scope. Worse, there are differences between Prolog systems that support modules with some flags being local to a module in a system and global in another. A notable case are `op/3` directives, which are local to modules in some systems and global in others.

### Enforcement of encapsulation

Most Prolog module systems allow any predicate to be called using explicit qualification. This is usually not an issue when  coding guidelines are enforced by strong team discipline. Logtalk, instead of relying solely in good practices, enforces encapsulation and generates an error on any attempt to call a predicate that is out of scope. Logtalk also prevents using specially crafted meta-predicates to break encapsulation and using code loading order to hack an object or category predicate to become multifile.

### Strict compiler

Most Prolog compilers are permissive, silently accepting problematic code. The Logtalk compiler is strict and either rejects or warns the user of a [large number of code issues](tools.html#lint-checker), contributing to earlier detection and warning of source code issues.

### Objects subsume modules

Logtalk objects *subsume* Prolog modules but the reverse is not true in general. You can't go from an object solution to a module solution easily or without significant hacking when you're taking advantage of e.g. inheritance, self and super calls, protocols, or parametric objects. Using a more general solution is worthy by itself and orthogonal to the programming in the small/large perspective.

As Prolog modules *are* objects, prototypes to be exact, most module-based solution can be easily translated into an object-based solution. So easy in fact that the Logtalk compiler does it for you (minus proprietary stuff that choke it, which varies from Prolog system to Prolog system; blame lack of standardization).

```logtalk
:- module(foo, [bar/1, baz/2]).
...
```

or

```logtalk
:- module(foo, []).
:- export([bar/1, baz/2]).
...
```

is simply interpreted by the Logtalk compiler as:

```logtalk
:- object(foo).
    :- public([bar/1, baz/2]).
    ...
:- end_object.
```

The Logtalk code is as readable as the module code, provides the same performance, and requires just one more directive, `end_object/0`, that any decent editor will type for you by expanding an object template. Note, however, that Logtalk does not use a predicate prefixing mechanism and does not provide the predicate exporting semantics found in Prolog modules. Thus, the interpretation of modules as objects is not a just a case of alternative syntax but results in different predicate **usage** semantics: by compiling a Prolog module as a Logtalk object, the exported predicates become public predicates that must be called either using the `::/2` message sending control construct or using an `uses/2` directive to list them as implicit messages to the object.

### Portability

Logtalk is written in highly portable code and currently supports [12 backend Prolog systems](download.html#requirements). It can support any Prolog system that complies with official and de facto core standards. Logtalk libraries and [developer tools](tools.html) are also portable.

In contrast, the ISO Prolog standard for modules is ignored (for sound reasons) by Prolog implementers. Worse, Prolog systems implementing a module system have significant differences that hinder portability. A few examples:

* ECLiPSe - no `module/2` directive
* SICStus Prolog and XSB - no `reexport/1-2` directives
* ISO standard - no `use_module/1-2` directives
* SWI-Prolog - operators are local to modules
* SICStus Prolog - operators are global
* XSB - atom-based module system
* ECLiPSe, SICStus Prolog, SWI-Prolog, YAP - predicate-based module system

But even when two Prolog systems provide the same syntax constructs, different semantics exist. For example, in ECLiPSe the `ensure_loaded/1` directive is equivalent to a `use_module/2` directive with an empty list of imported predicates while in SWI-Prolog the `ensure_loaded/1` directive is equivalent to a `use_module/1` directive.

In addition, not all Prolog systems implement modules. Examples include B-Prolog, CxProlog, GNU Prolog, and Qu-Prolog. Logtalk highly portable code works as-is and independently of the presence or absence of a module system.

### Key mechanisms

Logtalk provides **fully portable** implementations of key mechanisms to all supported backend Prolog compilers. These include:

* Conditional compilation
* Term-expansion
* Message printing
* Question asking

Conditional compilation directives are found nowadays in most Prolog systems although some implementations are buggy, including in some high profile systems, if you need more than the very basic usage.

The term-expansion mechanism can be traced back to Quintus Prolog. Nevertheless, it is only found in some of the supported systems but with proprietary variations that hinder portability. The Logtalk implementation, besides being portable and working the same in all supported systems, provides improved functionality that subsumes most existing implementations and allows fine control of expansion pipelines.

The message printing mechanism can also be traced back to Quintus Prolog. But it is only supported by some Prolog systems. The Logtalk implementation extends the original implementation by introducing a _component_ argument that allows easy filtering of messages per component in large applications and helps avoiding message term conflicts between components. It also provides support for _meta messages_ avoiding the need of defining grammar rules for translating each and every message as in the original implementation.

The question asking mechanism is original to Logtalk and the dual of the message printing mechanism. It allows abstracting asking questions to a user in the same way that the message printing mechanism abstracts printing messages to the user. It is an uncommon mechanism. But it facilitates abstracting applications input/output interfaces while also allowing common requested features such as logging to be plugged in.


## Why not Logtalk?

Logtalk materializes a number of design choices that may not be ideal for some Prolog programming scenarios.

### Increased startup times

Starting a Logtalk application requires loading both the chosen backend Prolog system and the Logtalk compiler and runtime. This necessarily increases the time it takes to start an application. This may be an issue where very fast startup times are required (of course, this is only meaningful if the applications themselves are small compared with the size of the Logtalk compiler and runtime). Note, however, that the Logtalk compiler and runtime can be precompiled by some Prolog systems for faster loading thus minimizing startup time (e.g. SWI-Prolog supports a Quick Load Format, QLF). The same solution when available can be applied to a Logtalk application.

### Increased application compilation times

Currently, Logtalk is implemented as a trans-compiler to Prolog. This means that a Logtalk source file is compiled into an intermediate Prolog source file that in turn is compiled using the chosen backend Prolog compiler, thus potentially increasing application compilation times compared with a Prolog only solution. That said, a portable _make_ tool is provided to limit source file recompilation to only changed files helping minimizing compilation time during development. Note that a comparison of application compilation times is only meaningful, however, for applications that don't take advantage of Logtalk unique features.

### Compatibility with Prolog native tools

Although Logtalk provides a complete set of [developer tools](tools.html), it only supports [selected](tools.html#third-party-tools) native Prolog developer tools.
Complex applications may require using both Logtalk and Prolog tools, demanding that the programmer learns how to be productive with a larger number of tools.

### Dynamic binding performance

Logtalk applications making heavy use of dynamic binding may require a backend Prolog compiler with good predicate clause indexing for best performance.

### No implicit predicate imports

Logtalk favors resilience to changes over convenience and thus does not support implicit predicate imports as in the Prolog `use_module/1` directive. In objects (and categories), only `use_module/2` directives (or its Logtalk equivalent, the `uses/2` directive) can be used. The practical consequence is that you need to use a `use_module/2` directive for implicitly calling module predicates and a `uses/2` directive for implicitly sending messages to objects. I.e. you need to either explicitly list the predicates or use explicit message sending. This can make the code a bit more verbose but it also prevents applications from breaking when new library predicates are implemented.

Note: the adapter files for some Prolog systems are able to convert in the fly `use_module/1` directives into `use_module/2` directives in some cases. This, however, is not recommended for the reasons stated above.

### Temporary files

The Logtalk compiler generates temporary Prolog files when compiling and loading source files. By default, these temporary files are kept out of the way and automatically deleted. This requires Logtalk to either work from a writable volume or to define the operating-system temporary directory as the scratch directory. As all common operating-systems natively provide a directory for temporary files, this is not considered an actual limitation although it is worth noting characteristic. Note that running embedded Logtalk applications doesn't not require any runtime compilation of the application source files (as embedding is accomplished using precompiled code).
