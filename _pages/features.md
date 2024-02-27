---
layout: article
permalink: features.html
title: Features
aside:
  toc: true
---

Logtalk is a  *declarative object-oriented logic programming language* that
can use most Prolog implementations as a backend compiler. It provides code
encapsulation and code reuses features for programming in the large. It
doesn\'t provide, or attempt to bring to Prolog, any notion of mutable state
that is not already available in plain Prolog or with Prolog modules. Logtalk
main features include:


### Protocols (interfaces)

Separation between interface and implementation is supported. Predicate
directives (declarations) can be contained inside *protocols* (interfaces),
which can be implemented by any number of objects (and categories). Protocols
are first-class entities, alongside objects and categories.


### Parametric objects (and categories)

Object (and category) identifiers can be compound terms containing free
variables that can be used to parametrize object (or category) predicates.
Notably, this allows the interpretation of predicate clauses as providing
*instantiations* of a parametric object identifier. I.e. using a parametric
object we can associate any number of predicates with a compound term.
Parameters are logical variables shared with all object (and category)
directives and clauses.


### Prototypes and classes

Both class-based and prototype-based systems are supported.
You may have, in the same application, class-based hierarchies
(with instantiation and specialization relations) and
prototype-based hierarchies (with extension relations). Moreover,
fundamental language features such as protocols (interfaces) and
categories (components) can be used simultaneously by classes,
instances, and prototypes.


### Multiple object hierarchies

No need to be constrained to a single, lengthy hierarchy rooted in
some generic object.


### Private, protected, and public inheritance

Logtalk supports private, protected, and public inheritance in a
way similar to C++. Moreover, any entity relation can be qualified
using a scope keyword. E.g. an object can *privately* implement a
protocol, thus making all protocol declared predicates private.


### Private, protected, and public predicates

Set the scope of your object predicates to match your protocol
design and let the runtime system enforce your choices.


### Static and dynamic objects

Objects can be either static or dynamic. Static objects are
defined in source files which are compiled and loaded in the same
way as Prolog files. Dynamic object can be either defined in
source files or created at runtime.


### Static and dynamic predicates

Any static object may contain both static and dynamic predicates.


### Based on standard Prolog syntax

Logtalk uses standard Prolog syntax with the addition of a few
operators and directives for a smooth learning curve. Prolog code
can be easily encapsulated inside objects with little or no
changes. Moreover, Logtalk can transparently interpret most Prolog
modules as Logtalk objects for easy reusing of existing code (e.g.
libraries).


### Lambda expressions

Native support for lambda expressions, including currying.


### Event-driven programming

Predicates can be implicitly called when a spied event occurs,
allowing programming solutions which minimize object coupling. In
addition, events provide support for behavioral reflection and can
be used to implement the concepts of *pointcut* and *advice* found
on Aspect-Oriented Programming.


### Component-based programming

Predicates can be encapsulated inside *categories*, which can be
virtually imported by any object, without any code duplication and
irrespective of object hierarchies. Thus, objects may be defined
through composition of categories, which act as fine-grained units
of code reuse. A category may also extend an existing category.
Categories can be used to implement *aspects* and mixin-like
behavior without resorting to inheritance. Categories also support
*hot-patching* of running code.


### Multi-threading programming

High level multi-threading programming is available when running
Logtalk with selected backend Prolog compilers, allowing objects
to support both synchronous and asynchronous messages. Threaded
engines, independent and-parallelism, and competitive
or-parallelism are also supported. Easily take advantage of modern
multi-processor and multi-core computers without bothering with
the details of creating and destroying threads, implement thread
communication, or synchronizing threads.


### Multi-inheritance and multiple-instantiation support

Logtalk supports multi-inheritance of both protocol and
implementation. An object may implement several protocols and
extend, specialize, or instantiate several objects.
Multi-inheritance conflicts can be solved implicitly by the
Logtalk lookup algorithms or explicitly by using predicate
directives.


### Good performance

Logtalk code is compiled using the same technics that you use to
write efficient Prolog code. In addition, Logtalk supports both
static binding and dynamic binding (with method lookup caching),
greatly improving performance. Benchmark results for some Prolog
compilers are available [here](performance.html).


### Close integration with Prolog standards

Logtalk is designed for smooth integration with any Prolog
compiler that conforms or closely follows official and de facto
Prolog standards.


### Compatible with most Prolog compilers

Logtalk interfaces with a specific backend Prolog compiler via a
minimal configuration file making it compatible with almost any
modern compiler.


### Comprehensive set of developer tools

The Logtalk distribution includes make, linting, debugging, documenting,
diagraming, testing, assertion, profiling, porting, metrics, versioning,
and packaging [developer tools](tools.html). Several of these tools can
also be [applied](using_tools_with_prolog.html) to plain Prolog and Prolog
module code bases.
