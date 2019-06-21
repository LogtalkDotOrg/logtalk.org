---
title: Prolog compilers are too permissive
author: Paulo Moura
layout: article
tags:
  - portability
show_edit_on_github: false
aside: false
---

Prolog compilers are too permissive, too forgiving&#8230; resulting in sloppy programming. Experienced programmers may shake off guilty feelings convincing themselves that's only run-once code that nobody is going to reuse, or port, or maintain. Or that's really not their fault. After all, if the Prolog compiler doesn't complain and the application appears to run, why care? Novice programmers never notice until they decide to switch Prolog compilers. Or when someone comes along and asks "what if" when trying to help them debugging or porting their applications.

Consider a simple example, the `arg/3` built-in predicate. Some popular Prolog compilers have long interpreted a negative term argument position as a failure rather than a programming error. When I complained (I used to do that a lot to Prolog implementers) the reply was something along the lines "we agree but our users would be upset if we break compatibility with their applications". You can easily find similar examples. Just dig into your memories. E.g. do you remember when "logical update semantics" come along all those applications relying on "immediate update semantics" suddenly broke?

Recently I ported, or tried to port, well known Prolog libraries and interesting Prolog applications to Logtalk, both to allow running these libraries and applications in most Prolog compilers and for testing the Logtalk automatic compilation of Prolog modules as Logtalk objects (oh the pain I choose to inflict upon myself!). Common sins are missing `discontiguous/1` and `multifile/1` directives, non-declared dependencies, i.e. missing `use_module/1` or `use_module/2` directives, arbitrary goals used as directives (instead of disciplined use of the `initialization/1` directive), duplicated predicate exports (specially when re-exporting predicates from imported modules), operator overdoses, term expansion clauses defined in the same file that is going to be term expanded (suddenly predicate definition order in a source file is important!), not to mention code relying on assumptions that are specific to a Prolog compiler or an operating-system. Prolog compilers should warn the users about these (and other) issues.

Another problem is hidden dependencies in Prolog "modes". Some Prolog compilers support an "iso" mode (that usually is not the default) and some other modes for backwards compatibility. Guess what happens when users try to reuse libraries developed for the same Prolog compiler but using different modes. Or when users startups the Prolog compiler in the wrong mood&#8230; err mode. If they are lucky, they will get a stream of compilation errors.

This is a vicious circle. Prolog implementers are afraid to make their compilers more strict because they don't want to break existing code or upset users. Users enjoy a permissive and flexible programming environment, even if they risk shooting themselves in the foot, unconsciously write non portable code, and have trouble listing their own code dependencies without using a cross-reference tool; they have little incentive and see no rewards in writing more portable and robust code.

Portability is not the only victim here. Is hard to do static code analysis (you want your applications to run faster and use less memory, don't you?) in this mix of explicit and implicit programming assumptions. ISO standardization is another victim as Prolog implementers and library developers get defensive arguing that the required changes are only of interest to ISO nitpicks, failing to see the forest behind their own tree.

This post is a bit harsh, I know. But wake-up calls sometimes need harsh voices to complement more carrot-like incentives and initiatives. Please don't shoot the messenger.
