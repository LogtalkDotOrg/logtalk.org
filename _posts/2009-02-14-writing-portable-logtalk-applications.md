---
title: Writing portable Logtalk applications
author: Paulo Moura
layout: article
tags:
  - portability
show_edit_on_github: false
aside: false
---

Portable Logtalk applications often need to call built-in predicates whose name, arguments, and semantics differ for each supported back-end Prolog compiler. This is quite frequent as the current Prolog ISO standard only covers basic functionality. A common solution for these cases is to define a protocol abstracting common functionality and to implement this protocol in a set of objects, one for each back-end Prolog compiler. An alternative solution is to use Logtalk conditional compilation directives. As also found in some Prolog compilers (e.g. ECLiPSe, SWI-Prolog, or YAP), Logtalk supports `if/1`, `elif/1`, `else/0`, and `endif/0` directives. The arguments of the `if/1` and `elif/1` directives are goals that are evaluated at compilation time, switching on and off the compilation of blocks of code. Together with the `prolog` read-only compiler flag, it is easy to define a single object encapsulating code for different back-end Prolog compilers. For example, assuming that your portable Logtalk application (running on GNU Prolog, SWI-Prolog, and YAP) needs access to the CPU time in seconds, you could write:

```logtalk
:- object(timing).

    :- public(cpu_time/1).
    :- mode(cpu_time(-number), one).
    :- info(cpu_time/1, [
        comment is 'Current CPU time in seconds',
        argnames is ['Seconds']]).

    :- if(current_logtalk_flag(prolog, gnu)).
    cpu_time(Seconds) :-
        cpu_time(Miliseconds),
        Seconds is Miliseconds/1000.

    :- elif(current_logtalk_flag(prolog, swi)).
    cpu_time(Seconds) :-
        Seconds is cputime.

    :- elif(current_logtalk_flag(prolog, yap)).
    cpu_time(Seconds) :-
        statistics(cputime, [Miliseconds, _]),
        Seconds is Miliseconds/1000.

    :- else.
    cpu_time(_) :-
        throw(error(resource_error(predicate), cpu_time/1)).

    :- endif.

:- end_object.
```

A second example, [cc](http://svn.logtalk.org/viewvc.cgi/trunk/examples/cc/), can be found on the current Logtalk distribution.

The conditional compilation directives can be used anywhere, as long as they encapsulate groups of directives or predicate clauses. Both solutions, using an object per back-end Prolog compiler or a single object with conditional compilation directives, have their pros and cons. The hard work, however, is usually to find the best abstraction subsuming the diversity of implementations.
