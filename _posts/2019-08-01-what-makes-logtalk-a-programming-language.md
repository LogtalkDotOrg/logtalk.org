---
layout: article
title: "What makes Logtalk a programming language?"
tags:
  - semantics
  - language
show_edit_on_github: false
aside: false
---

Logtalk is currently implemented as a [*transpiler*](https://en.wikipedia.org/wiki/Source-to-source_compiler) to Prolog. This is a sensible choice given that Logtalk is *designed* to extend Prolog with better code encapsulation and code reuse mechanisms while leveraging all other great Prolog features. Writing the transpiler in highly portable Prolog code enables running Logtalk with most Prolog systems. It also allows using most native Prolog resources (e.g. libraries) from within Logtalk applications (sharing of resources is a common goal of trans-compiled languages).

Logtalk is just one of several languages implemented as a transpiler. Historical examples include C++, which started as a transpiler to C named [Cfront](https://en.wikipedia.org/wiki/Cfront), and Erlang, which was [initially implemented](http://www.erlang-factory.com/upload/presentations/389/EFSF11-ErlangVM.pdf) in Prolog. Although a language implementation is mainly a technical (rather than definitional) aspect, I regularly come across people downplaying Logtalk with the justification that is implemented as a transpiler and thus no more than a term rewriting exercice. Interestingly, this argument is mainly raised by Prolog implementers and vendors, suggesting some discomfort. The irony here is that only mature languages are practical for implementing other languages.

Resisting the weak and distracting argument of mistaking a language for its implementation, what separates Logtalk from a Prolog library? And, while we're at it, what about e.g. CHR, CLP(FD), or even DCGs? Can these also be sensibly classified as languages, even if used embedded in Prolog? The interesting metric here is *semantics*. Drawing lines can be an entertaining academic exercice by itself but there's a more worthy topic with practical impact: what does Logtalk, CHR, ... have to offer to Prolog programmers?

Let's start with DCGs. Grammar rules are used to *thread state* between predicate calls where the arguments carrying the state are abstracted. I.e., grammar rules are an *abstraction* over predicate clauses. The syntax rewrite of grammar rules into clauses doesn't require extending the Prolog runtime or introducing new semantics. In particular, the standard `phrase/2-3` predicates, used to call a grammar rule, are strictly not required given the details of the syntax rewrite. This rewrite can easily be done manually although it would be tedious and error prone, resulting in less readable code.

CLP(FD) is a different case. Arithmetic constrains are not an abstraction over the standard Prolog arithmetic evaluation and comparison predicates. Constraints require changes to the Prolog runtime (usually materialized with the help of term unification hooks). Without those changes, constraints would not be propagated, narrowed, or solved when proving a goal. Thus, CLP(FD) and other constraint systems add semantics not present in standard Prolog (note that constraints were introduced in early Prolog systems, notably Prolog III, but that's a topic for another post).

What about Logtalk? Objects, protocols, and categories are not an abstraction over Prolog modules. I.e. Logtalk entities semantics differ significantly from Prolog modules semantics. Message sending is not the same as module-qualified calls. Logtalk clear distinction between *declaring* and *defining* a predicate doesn't exist in Prolog but it's key for the fundamental concept of protocol. Modules don't (commonly) enforce encapsulation. There's no equivalent in module systems to parametric objects. No equivalent to inheritance semantics (despite some [bogus claims](half-broken-hacks-reexport-as-inheritance.html)).

Understanding Logtalk/CHR/CLP(FD)/DCGs/... abstractions/semantics/programming idioms/patterns/... allows you, as a developer, to take on a wider range of problems and to explore and construct solutions that go beyond what core Prolog features have to offer. Isn't that what really matters?
