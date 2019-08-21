---
layout: article
title: "New developer tool: tutor"
tags:
  - tools
  - learning
show_edit_on_github: false
aside: false
---

Learning a new programming language can be both thrilling and daunting. Your shiny new programs may run beautifully on the first try but may also trigger a barrage of compiler warning and error messages. All the sudden, you may be searching documentation, asking friends, posting pleas for help, trying to understand where it all gone wrong. Sometimes the issues are easy to diagnose from the warning or error message text and location. Sometimes you're left scratching your head. Assumptions carried from other languages can easily lead you into the wrong path.

Most language compilers output terse compiler warning and error messages. Seasoned developers immediately recognize the issues and know how to fix them. The compiler terseness is a plus for them as it cuts down the output and noise to the strictly necessary. Not so for the newbies that the language and compiler authors want to win over.

Logtalk and some Prolog systems design enable an elegant solution that allows us to cater to both experienced developers and new users: the [message printing mechanism](https://logtalk.org/manuals/userman/printing.html). This mechanism provides an abstraction over the printing of messages where each message can be intercepted and thus diverted, rewritten, suppressed, or *extended*. The Logtalk compiler uses this mechanism to print warning and error messages. Logtalk 3.28.0 (released in August, 2019) includes a new [tutor tool](https://logtalk.org/manuals/devtools/tutor.html) that's trivial to use (you just need to load it at startup, usually from your [settings file](https://logtalk.org/manuals/userman/installing.html#settings-files)) and that intercepts and extends most compiler warning and error messages with explanations and suggestions.

Let's see some examples of the `tutor` tool in action. Assume that a new user wrote the following `foo.lgt` source file:

```logtalk
:- object(foo).

    :- public(bar/0).
    bar :-
	    baz(a).

    baz([]).
    baz([_| _]).

:- end_object.
```

The Logtalk compiler will diligently print the following warning:

```text
?- {foo}.
*     No matching clause for goal: baz(a)
*       while compiling object foo
*       in file /Users/pmoura/foo.lgt between lines 4-5
*     
% [ /Users/pmoura/foo.lgt loaded ]
% 1 compilation warning
true.
```

This particular warning is reasonably self-explanatory. Still, if we preload the `tutor` tool, we will get instead:

```text
?- {tutor(loader)}.
...
% (0 warnings)
true.

?- {foo}.
*     No matching clause for goal: baz(a)
*       while compiling object foo
*       in file /Users/pmoura/foo.lgt between lines 4-5
*     Calls to locally defined predicates without a clause with a matching head
*     fail. Typo in a predicate argument? Predicate definition incomplete?
*     
% [ /Users/pmoura/Desktop/foo.lgt loaded ]
% 1 compilation warning
true.
```

In this case, the `tutor` tool not only explains the consequence of not fixing this warning but also makes some suggestions on possible causes. Besides an opportunity to explain language semantics, as in the above example, the tool can also leverage the compiler linter to introduce e.g. coding guidelines:

```text
*     Non-terminal name in camel case: noMoreTokens//0
*       while compiling object naming
*       in file /Users/pmoura/logtalk/examples/errors/warnings.lgt at or above line 464
*     Coding guidelines advise the use of underscores
*     to separate words in non-terminal names.
```

Most errors messages are also extended with explanations and suggested fixes. For example:

```text
!     Permission error: modify object_alias baz
!       in directive uses/1
!       in file /Users/pmoura/logtalk/examples/errors/modify_object_alias.lgt between lines 23-26
!     This name is already declared as an alias to another object.
!     Typo in the alias or the object name?
```

Hope you enjoy this new tool, specially if you're learning Logtalk or using it in a classroom. The tool is still in development and there may be some compiler warning and error messages that are not yet explained or whose explanations can be improved. As always your feedback and suggestions are most appreciated.

P.S. You can get a good overview of the tool by playing with the [`errors`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/errors) example, whose purpose is to illustrate compiler errors and warning messages.
