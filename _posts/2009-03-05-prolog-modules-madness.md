---
title: Prolog modules madness
author: Paulo Moura
layout: article
tags:
  - semantics
  - modules
  - portability
show_edit_on_github: false
aside: false
---

Try the following experiment in a Prolog compiler supporting modules such as SWI-Prolog or YAP. Define two modules that export the same predicate and try to load them. For example, assume a file `m1.pl` with content:

```logtalk
:- module(m1, [p/1]).

p(X) :- clause(X, true).

:- dynamic(a/1).
a(one). a(two). a(three).
```

and a file `m2.pl` with content:

```logtalk
:- module(m2, [p/1]).

p(X) :- clause(X, true).

:- dynamic(a/1).
a(1). a(2). a(3).
```

Let's try to load these two files in SWI-Prolog:

```text
$ swipl
Welcome to SWI-Prolog (Multi-threaded, 32 bits, Version 5.7.7)
Copyright (c) 1990-2008 University of Amsterdam.
SWI-Prolog comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to redistribute it under certain conditions.
Please visit http://www.swi-prolog.org for details.

For help, use ?- help(Topic). or ?- apropos(Word).

?- [m1, m2].
% m1 compiled into m1 0.00 sec, 1,316 bytes
ERROR: Cannot import m2:p/1 into module user: already imported from m1
false.

[debug]  ?- 
```

We get an error. It seems that loading a module automatically imports its exported predicates into the loading context (the module `user` in this case). How unfortunate. We don't get a chance of using explicit qualified calls to choose which predicate to call. Let's try the same experiment with YAP:

```text
$ yap
% Restoring file /usr/local/lib/Yap/startup
YAP version Yap-5.1.4
   ?- [m1, m2].
 % consulting /Users/pmoura/m1.pl...
 % consulted /Users/pmoura/m1.pl in module m1, 1 msec 1056 bytes
 % consulting /Users/pmoura/m2.pl...
 % consulted /Users/pmoura/m2.pl in module m2, 0 msec 648 bytes
NAME CLASH: m1:p/1 was already imported to module user;
            Do you want to import it from m2 ? [y or n] 
```

In this case, we get a prompt asking what to do. Maybe interesting if we happen to be in an interactive session, otherwise&#8230;

Ciao have claimed for a long time to provide a better module system so let's try a similar experiment with this compiler. This time we explicitly say that we want to use both modules:

```text
$ ciao
Welcome to the Ciao Prolog Development System!

Ciao-Prolog 1.10 #8: Wed Jan 31 21:54:06 WET 2007
?- use_module(m1), use_module(m2).

yes
?- p(a(X)).

X = one ? ;
X = two ? ;
X = three ? ;
no
```

In this case, there is no error, no prompt, the compiler just silently makes a choice in our behalf. How can the compiler know how to make the right choice? Should the order of the `use_module/1` calls really matter? What if there are two exported predicates with the same name in both modules and we want one from the first module and the other from the second module?

What these experiments tell us?

Prolog compilers automatically import, or try to import, the exported predicates of loaded modules. Therefore, whenever two modules export the same predicate, we either get an error (SWI-Prolog), a prompt for solving the conflict (YAP), or automatic conflict resolution (Ciao). So much for the often proclaimed _de facto_ module standard.

Modules are supposed to provide namespaces. Except, it seems, for their exported predicates. In this case, a module developer needs to be aware of all the exported predicates in all modules that might be used by him, or by her, or by third parties in order not to get into trouble. Or risk the chance of getting his or her users into trouble. This is the amazing foundation that many implementers and users alike feel that should be used to build the predicate libraries that will support our Prolog applications. My biggest problem is, of course, how to hide this post from colleagues working in other programming languages. I don't want them to laugh themselves to death.
