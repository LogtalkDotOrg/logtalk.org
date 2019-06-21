---
title: Logtalk 2.36.0 released
author: Paulo Moura
layout: article
tags:
  - portability
show_edit_on_github: false
aside: false
---

I released Logtalk 2.36.0 yesterday. The biggest news is support for _settings files_. At startup, Logtalk looks for and loads a `settings.lgt` file found in the startup directory. If not found, Logtalk looks for a loads a `settings.lgt` file in the Logtalk user folder. These settings files allows users to customize Logtalk without forcing them to edit the back-end Prolog configuration files, which often change between releases. This allows users to easily update to a new Logtalk version without the tedious work of reapplying changes to the default values of compiler flags to the new versions of the configuration files. Updated scripts and installers automatically will take care, for future releases, of preserving any existing settings file found when updating the Logtalk user folder.

Although the new settings files feature is easy to describe, a lot of work went into implementation and testing, thanks to the lack of Prolog standards for operating-system access. This includes basic functionality such as finding out the startup directory, opening a file in the current directory, and accessing operating-system environment variables. Something that should be implemented and tested during an afternoon, took me one week of work. One week that would be better spent working on e.g. the Logtalk libraries. In the end, I got settings file working for most back-end Prolog compilers on POSIX systems and, for some of them, also on Windows. Not ideal but hard to do better giving the back-end Prolog compiler limitations.

Lack of feature-parity between back-end Prolog compilers is always a problem. It turns what should be simple documentation in long lists of exceptions. Some users, completely oblivious of the nightmare that is writing portable Prolog code, end up blaming Logtalk for a limited feature set that pales when compared with recent programming languages. I'm quite tired of dealing with this portability problems. Therefore, future Logtalk releases will cut down on the number of compatible Prolog compilers. Hopefully, this will speed up future development and will enable more straightforward implementations of new functionality.
