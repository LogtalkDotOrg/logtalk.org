---
layout: article
title: Modules are objects
tags:
  - modules
show_edit_on_github: false
aside: false
---

**Prolog modules are objects.** This statement may surprise you. From past experience, it will also annoy some Prolog practitioners. It is not the case that the creators of Prolog module systems *intended* to create an object-oriented extension to Prolog. But what modules *are* is a function of their *characteristics*, not a function of its *design intentions* <sup id="a1">[1](#f1)</sup>.

There is a partial but widespread view of not only OOP being a synonymous of imperative OOP but also OOP languages being a synonymous of *class-based* languages. This often leads to the idea that Prolog modules are fundamentally distinct from objects. But OOP can also be declarative (as exemplified by Logtalk) and OOP languages can also be *prototype-based* (e.g. Self and JavaScript) instead of *class-based*. It turns out that **modules systems define a simple, limited, *prototype-based* OOP language**.

How is the OOP notion of a *prototype* materialized by a Prolog module? Let's consider the defining characteristics of a prototype one-by-one:

##### Identity

This is the most basic characteristic of an object in any OOP language. It's also a basic characteristic of Prolog module systems that each module have a unique identity (an atom).

##### Creation

Prototypes can be created *ex-nihilo* (i.e. from scratch). Likewise, a Prolog module can be defined in a source file or dynamically created at runtime. For example, the following query creates a module named `foo` in most module systems (a notable exception being the ECLiPSe module system):

```text
?- foo:assertz(bar).
```

Prototypes can also be created by expressing how they differ from other prototypes, know as their parent prototypes. With modules, we can use the `reexport/1-2` directives to achieve similar functionality <sup id="a2">[2](#f2)</sup>.

##### Messages

Although explicitly-qualified module predicate calls don't perform the lookups associated with messages, they can still be interpreted as messages in a prototype system. With a standalone prototype, message lookup only considers the prototype itself. 
Likewise, if a module doesn't reexport other modules (or reexport predicates from other modules), implicit or explicitly, them an explicitly-qualified predicate call only checks the module itself. When a prototype extends (or is derived from) other prototypes, message lookup will follow the derivation chain(s). Likewise, if a module reexports other modules (or reexports predicates from other modules), an explicitly-qualified predicate call will work for any predicate in the reexport chain(s).

**QED**

Note: the main motivation for this blog post is the well intended advice of people in the community that Logtalk is handy *when you need some OOP* in your Prolog application. This advice completely misses the point. Logtalk objects (which are capable of playing the role of both classes and prototypes) subsume Prolog modules and can do everything Prolog modules do and much more with elegance and aplomb.

---

<b id="f1">1</b> Here we will only be discussing *predicate-based* Prolog modules. A few Prolog modules systems are *atom-based* (e.g. XSB) but comparing them is a topic for another post. [↩](#a1)

<b id="f2">2</b> Using `reexport/1-2` directives to implement inheritance is a [know half-broken hack](https://logtalk.org/2019/06/26/half-broken-hacks-reexport-as-inheritance.html) but that's beside the point here. [↩](#a2)
