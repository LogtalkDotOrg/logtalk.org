---
title: Logtalk 2.37.2 released
author: Paulo Moura
layout: article
tags:
  - community
show_edit_on_github: false
aside: false
---

I released Logtalk 2.37.2 a couple of days ago. This is the third incremental release of the 2.37.x version. A total of 37 major releases, 122 when including both major and minor releases, since I started the Logtalk project in January of 1998 (the number 2 means this is the second generation of the Logtalk language; generation 3 is coming in a not so distant future). Release 2.37.3 is already being developed. This is your typical example of the open source mantra _release often, release early_.

The wide Prolog compatibility goals of Logtalk means that there is really no end in sight for Logtalk development. Sometimes this scares me. At other times, it pushes me out of bed. It also means that an wealthy number of Prolog compilers are alive and kicking, continuously being improved. Many of the changes in this and past releases are Prolog compatibility updates. Lack of strong standardization only complicates matters.

This release takes Logtalk support for compiling Prolog modules to a new level. This support is important for a number of reasons. First, it shows that Logtalk is not only a superset of plain Prolog but also of Prolog plus modules. Within reasonable terms, of course, giving that Prolog module dialects often remind me of the Babel tower tale. Second, compiling a module as a Logtalk object helps to identify potential problems when porting Prolog code to Logtalk. Testing of this feature include compiling, or trying to compile, several Prolog modules libraries and non-trivial Prolog module applications such as [TopLog](http://www.doc.ic.ac.uk/~jcs06/TopLog/) and [ClioPatria](http://e-culture.multimedian.nl/software/ClioPatria.shtml). Results are good despite some [unfortunate problems](../../06/26/prolog-compilers-are-too-permissive.html) in the original Prolog module code. Third, all the trouble in implementing this feature helps to improve the Logtalk code base, making it more robust, allowing it to cope with a diversity of programming practices. Fourth, it helps me to better understand the subtleties of specific Prolog module systems, something that often is not easy to learn just by sitting down and reading user manuals. One always learns good bits to adapt and pitfalls to avoid when studying other people's code.

Hope you enjoy this new release.

P.S. Is great to finally get some free time to post some thoughts on Logtalk development after a very tiresome teaching semester. I keep dreaming about doing Logtalk development full time. Maybe one of these days&#8230;
