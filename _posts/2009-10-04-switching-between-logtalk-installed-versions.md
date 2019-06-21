---
title: Switching between Logtalk installed versions
author: Paulo Moura
layout: article
tags:
  - development
show_edit_on_github: false
aside: false
---

Recent Logtalk releases include a shell script, `logtalk_select`, which allows easy switching between installed Logtalk versions. It's an experimental script, loosely based on the `python_select` script, with two major limitations: it doesn't update the Logtalk user folder and it's POSIX-only. Nevertheless, it's useful whenever you want to test your application with a new Logtalk release. Usage is quite simple. In order to list all installed versions type:

```bash
$ logtalk_select -l
Available versions: lgt2372 lgt2373 lgt2374 lgt2375
```

The current installed version can be checked by typing:

```bash
$ logtalk_select -s
Current version: lgt2375
```

In order to switch to another installed version type:

```bash
$ sudo logtalk_select lgt2374
```

Using `sudo` may or may not be needed depending on your Logtalk installation prefix and on the administrative privileges of your user account. Typing the script name without arguments prints a help script:

```bash
$ logtalk_select
This script allows switching between installed Logtalk versions

Usage:
logtalk_select [-vlsh] version

Optional arguments:
-v print version of logtalk_select
-l list available versions
-s show the currently selected version
-h help
```

If you're a shell scripting wizard and able to improve the `logtalk_select` script, please mail me. As always, feedback and contributions are most welcome.
