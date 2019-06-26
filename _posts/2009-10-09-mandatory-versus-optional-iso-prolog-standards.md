---
title: Mandatory versus optional ISO Prolog standards
author: Paulo Moura
layout: article
tags:
  - standard
  - modules
show_edit_on_github: false
aside: false
---

Currently, there are two approved ISO Prolog standards: ISO/IEC 13211-1: General core (first edition published in 1995-06-01; an errata was published recently) and ISO/IEC 13211-1: Modules (first edition published in 2000-06-01). There are also five standardization proposals being discussed: Core Revision, Definite Clause Grammars (DCGs), Globals, Threads, and Portable Operating-System Interface (POSI).

While I was a member of the WG17 standardization group (see my [previous post](../01/stepping-down-as-editor-of-iso-prolog-standardization-proposals.html)), I always stood for a mandatory core standard, making all other standards optional when talking about ISO compliance of a specific Prolog compiler. This means that a Prolog implementer would only need to comply with the core standard in order to claim conformance to the ISO Prolog specification. The Prolog implementer could also freely chose to implement e.g. DCGs and POSI, disregarding Module, Globals, and Threads.

This view of mandatory and optional Prolog standards was shared by some but not all members of the WG17 standardization group. Some of them want to make the Module standard mandatory and pushed for making some of the other standardization proposals dependent (or at least making reference to) the approved Module standard. I find this a recipe for disaster and for ISO Prolog standards irrelevance. A standard should stand on its own merits. Despite the hard work done on the Module standard, the proposed module system is (rightfully) ignored by most Prolog implementers. Other standard proposals should not be used as a leverage for forcing implementers to implemented a flawed standard.

Why is the current Module standard flawed?

First, it specifies a new module system instead of trying to standardize current practice. Instead of helping existing module implementations to converge, the standard choses to specify a new, and therefore incompatible, module system. For example, the standard introduces a new concept of module interface (which can only be implemented by a single module!) that is not found elsewhere, even today.

Second, it specifies two different and incompatible ways of dealing with meta-predicates (the infamous `colon_sets_calling_context` flag). This means that two Prolog compilers can comply with this standard and still be incompatible!

Third, specifies a meta-predicate directive that prevents the specification of the number of missing arguments when working with closures. One of the consequences is that only the Prolog implementer knows how to parse and make use of meta-predicate directive for built-in predicates! But check what the inventor of the meta-predicate directive have to [say](http://www.cs.otago.ac.nz/staffpriv/ok/pllib.htm) about the flaws on the meta-predicate directive as specified in the Module standard.

Fourth, it makes some poor choices regarding built-in predicates and built-in directives. For example, the specification of the `predicate_property/2` predicate defines the properties `public` and `private` as stating if `clause/2` can be used on the predicate clauses. Thus, the properties `public` and `private` cannot be used to infer about predicate scope, which would be a much better match for most programmer expectations. Another example is the meta-predicate directive, which is ugly named `metapredicate/1` (while existing module systems use, of course, a `meta_predicate/1` directive!).

Fifth, the standard fails to specify a solution for renaming predicates when importing. The consequence is that library developers need to be aware of the predicate names used by other library developers in order to avoid conflicts. So much for the idea that modules provide an encapsulation mechanism. Of course, the standard also states that any module predicate (including not exported ones) can be called using explicit qualification and leaves as "an allowable extension to provide a mechanism that hides certain procedures (&#8230;)".

Other problems with the current module standard could be described here but the ones stated above are hopefully enough to convince you that the standard needs to be thoroughly revised.

You may think that my critics of the current module standard (and WG17 policies) are mostly motivated by my work in Logtalk, which provides an alternative to the use of modules. You are wrong. True, Logtalk objects subsume module functionality and the Logtalk compiler is able to compile most modules as objects. But the Logtalk compiler also goes to great lengths to allow programmers to use both modules and objects in the same applications. Case in point: the fact that Logtalk can compile most modules as objects clearly show that there is enough common core functionality in today's module systems to warrant a new module standard focused in current practice. But any new or revised module standard should also pay due attention to the advanced modules found on some Prolog systems such as ECLiPSe and Ciao.

In its current state, making the current module standard mandatory or required for implementing other standard proposals will either delay standardization efforts or will tie implementations to a limited and flawed module system for years to come.
