---
title: How To Misappropriate and Misrepresent Other People's Hard Work in 12 Easy Steps
author: Paulo Moura
layout: article
tags:
  - community
show_edit_on_github: false
aside: false
---

**Step 1.** Work using an alias. Why expose your identity? 

**Step 2.** Spend years [asking](http://forums.logtalk.org/viewforum.php?f=14) the Logtalk open-source developer to implement everything except the proverbial kitchen sink, while at the same time politely declining to make any significant code contribution to all those features you find critical. After all, you're a commercial user, with serious business to attend to. No time to fool around. In our example, the wish list includes: 

  * an IDE
  * a type-checker
  * a cross-referencer
  * automatic dependency generation
  * a bootstrapped implementation
  * a code coverage tool
  * a web server
  * a sockets interface
  * unit test support (ignoring the existing one)
  * new documenting tools (as the existing ones don't fit your commercial development requirements)
  * a revamped debugger
  * ...

**Step 3.** Score hundreds of hours of free support, including on-line and in-situ, from the Logtalk developer. Besides saving you precious development time, you're also learning the fine details of the Logtalk implementation, which will be quite handy in later steps. 

**Step 4.** Plan your moves carefully. For example, make a peanuts donation to the Logtalk hosting expenses. It's one less burger and cola, which in itself is not a bad idea. Who knows? It might become handy in the future to claim that you had gone as far as contributing financially to the original project. 

**Step 5.** Try to dictate the Logtalk roadmap in a public Logtalk wiki. Users write wish lists; developers write roadmaps. But who cares about these fine distinctions? The important bit is that you may now argue that your "collaboration" attempts got shut down by the ungrateful Logtalk developer. 

**Step 6.** Fork Logtalk. Forks can be a fantastic tool for collaborative development. So much that Logtalk is available not only from an [open-access Subversion server](http://svn.logtalk.org/) but also from a [git repository](https://github.com/LogtalkDotOrg) in a convenient public place. Of course, a fork starts as being an exact copy of the existing software. 

**Step 7.** Take a page from Microsoft and name your fork [OpenLogtalk](http://wiki.github.com/ParkerJones/logtalk/). This will make it easier for new users to peek the most [open](https://logtalk.org/license.html) alternative. Is dead simple: just choose the one with "open" in its name. Duh! 

**Step 8.** Present your work as an upcoming professional alternative to the original academic and amateur one. Sprinkle the description of your fork with concepts from Software Engineering 101. Talk how you're going to provide "high reliability" and "comprehensive documentation". Talk is cheap; you can afford it. 

**Step 9.** Present your work as a new implementation, while kindly acknowledging the first and original implementation. For example, [write](http://github.com/ParkerJones/logtalk/commit/000ae7b011e25093f4daa206a129df46ff359fce): 

> OpenLogtalk is an implementation of the "Logtalk language".
> 
> The first implementation of Logtalk was by Paulo Moura.

The article "an" is a good choice as it nicely suggests "another" and "alternative". Don't let the little fact that the first implementation is also the only existing one, that you forked, spoil your message. Deception, after all, is an art that requires practice. 

**Step 10.** Make cosmetic changes to your fork. [Change tabs into spaces](http://github.com/ParkerJones/logtalk/commit/0d3490dda5bfad0b524bdce0999a42b3ecaa484f), [put a tab before comment text](http://github.com/ParkerJones/logtalk/commit/a71d90753b0407a60ac8742270a5015cdd44df63), [split files in smaller files](http://github.com/ParkerJones/logtalk/commit/21137e1102fada20c2b679fe352c1d3d49a3b71a) (nothing rhymes more with "modular" than a lot of small files, even if you just end up [loading all of them](http://github.com/ParkerJones/logtalk/blob/modules1/compiler/load.pl)), [remove a prefix from internal names](http://github.com/ParkerJones/logtalk/commit/2d858195ac26e70a6b7c4e8b4a49dbe219ad0631), never mind that is there for sound technical reasons as [already explained to you](http://forums.logtalk.org/viewtopic.php?f=13&t=115). 

These changes are very important as they (1) make the code in your fork look different in a quick glance; (2) make the code fit your programming style ([coding guidelines](https://github.com/LogtalkDotOrg/logtalk3/wiki/Coding-Guidelines) of the original developer be damned; it's your fork!); (3) make it next to impossible for the original developer to pull and include your changes without lots of rewriting work; (4) reinforce the reality distortion field that you jump-started in the previous steps. As a bonus, you may get to claim later on the road the the original developer is not playing nice as he is not picking up your "contributions". 

**Step 11.** Innocently ask the original developer for help in understanding the source code. Put his mail replies in [new files](http://github.com/ParkerJones/logtalk/commit/231ea6405963a01f7e56bc6843eda998ce0c01e7) in your fork. It helps in [product differentiation](http://github.com/ParkerJones/logtalk/commit/8cbcb51b34baf9cbb56e4a64eeeb48c8699fb241). 

**Step 12.** There is no step 12. You're already using a fork, not for collaborating, but to split. The best thing that can happen to a young programming community. Just let it roll. 

**P.S.** If you care about Logtalk, help to spread this post and expose the troll. 

Logtalk is the result of more than 12 years of hard work. Logtalk is, always have been, and always will be open for collaborations. Is not open, however, for abuse from disgruntled commercial users.
