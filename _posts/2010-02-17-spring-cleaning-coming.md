---
title: Spring cleaning coming
author: Paulo Moura
layout: article
tags:
  - portability
show_edit_on_github: false
aside: false
---

The development of the current generation of Logtalk, 2.x, began on January of 1998. At that time, the ISO Prolog Standard (Part 1: General Core) was only three years old. Thus, accepting and dealing with the lack of compliance of most Prolog compilers with the standard was a sensible choice.

Back to the present. The ISO Prolog Standard is now 15 years old. Compliance with the standard greatly improved for some but not all Prolog compilers. Trying to keep minimal Logtalk compatibility with some of the existing Prolog compilers is no longer feasible. In fact, keeping compatibility with the most problematic Prolog compilers (as far as standard-compliance goes) is working as an anchor, slowing Logtalk development and preventing improvements and implementation of new features.

Some of the most problematic Prolog compilers (again, from the point-of-view of standards compliance) are (to the best of my knowledge) no longer being developed. Other Prolog compilers, actively maintained today, decided to ignore the current official and de facto standards. A few, such as IF/Prolog, provided good standard compliance but have been apparently discontinued by their developers.

I plan to ditch Logtalk compatibility with the following Prolog compilers in the upcoming 2.39.0 release: ALS Prolog, Amzi! Prolog, BinProlog, GNU Prolog, IF/Prolog, JIProlog, K-Prolog, LPA MacProlog, LPA WinProlog, Open Prolog, MasterProlog, PrologII+, Quintus Prolog. This may seem like a long list but I suspect this decision will have no consequence for most (if not all) Logtalk users. If If you think it is still worth to support some compiler in this list please contact me as soon as possible.

UPDATE: added GNU Prolog to the list of no longer supported compilers. Support for this compiler will be restored as soon as it implements the ISO Prolog standard directive `multifile/1`.
