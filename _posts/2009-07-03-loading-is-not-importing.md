---
title: Loading is not importing!
author: Paulo Moura
layout: article
tags:
  - semantics
  - modules
show_edit_on_github: false
aside: false
---

Recently, I posted some [rumblings](../../06/26/prolog-compilers-are-too-permissive.html) about my experience compiling Prolog modules as Logtalk objects. One of my pet peeves with Prolog module systems and Prolog module code is the [unfortunate mix up](../../03/05/prolog-modules-madness.html) between _loading_ and _importing_. Is quite simple really, repeat after me:

> **Loading is not importing!**

If a user wants to load a module, the `ensure_loaded/1` directive shall be used. If the user want to import the public predicates of a module, the `use_module/1-2` directives shall be used. Sadly, this basic distinction between these two **orthogonal** operations is not enforced by most Prolog compilers with a module system (despite some advice found in Prolog user manuals). Moreover, the `ensure_loaded/1` directive shall only be used outside modules. Its semantics should simply be: load a file if not already loaded. There is no need for this directive to be the jack-of-all-trades. A simple test: if your Prolog compiler complains when you **load** two Prolog source files defining two different modules exporting the same predicate, then your Prolog compiler is broken. Complaining about conflicting imports only makes sense when **importing**. Otherwise a library developer would need to be omniscient about every other library developer work. Module encapsulation purpose is to avoid predicate name conflicts in the first place. Auto-importing public predicates when **loading** is equivalent to putting holes in module encapsulation. For what purpose? Is really that much trouble to use the `use_module/1-2` directives for **importing**? Sure, these directives also load a file if not already loaded. They must. After all, we are saying that we want to use a module! That doesn't mean that the `ensure_loaded/1` directive should work in retribution as a `use_module/1-2` directive in disguise!

As the [bible](http://en.wikipedia.org/wiki/KISS_principle) says, why complicate implementation, complicate documentation, complicate semantics? In order to perpetuate mix-ups? To ruin encapsulation goals? Just to cope with sloppy user programming?
