---
title: 'One of the obstacles to Prolog success is ...'
author: Paulo Moura
layout: article
tags:
  - modules
  - standard
show_edit_on_github: false
aside: false
---

&#8230; current module systems. The lack of a strong module standard is often touted as the reason behind the lack of portable Prolog libraries. Problem is, modules fail at everything that we want and need to accomplish when thinking about namespaces in Prolog. Data hiding? No, any module predicate can be called using explicit module qualification. You may think of a module predicate export list as the public module predicates but that's only wishful thinking. Portability? Only if you forgo the use of operators and meta-predicates and restrict yourself to a subset of the Prolog compilers implementing a module system. The fact that the current ISO Prolog standard for modules is incompatible with the module systems found on most Prolog compilers does not help either. Separation between interface and implementation? No, simply not possible. Conflicts between imported predicates? Compiler errors and warnings will usually tell you there is a problem but modules do not provide mechanisms for solving the conflict other than reordering of import directives (that can only solve some of the problems). Ever wondered why module predicates often use a functor with a prefix which usually is the name of the module? The preferred and recommended way of using modules is through import directives and implicit qualification. Thus, we cannot reuse vocabulary between modules in fear of name conflicts (think polymorphism). Most current Prolog module systems simply do not provide the building blocks needed for the development of portable Prolog libraries. Without portable libraries, users are easily trapped into a single Prolog implementation. Want to shop around for third party libraries? You will be hard-pressed to find even vaporware.

Rats! This post ended up being a rant. I will try to behave next time.
