---
layout: article
permalink: first_project.html
title: Your first project
aside:
  toc: true
---

Ready to start your first Logtalk project? Follow these simple steps and suggestions for smooth sailing. Additional, detailed advice can be found in the Logtalk [Handbook](https://logtalk.org/manuals/userman/programming.html).


## Basic setup

If you haven't done so already, when following the [learning guide](learning.html), start by copying the `settings-sample.lgt` found at the root of the Logtalk distribution to your home directory (or any other of the searched locations; see the comments in the file itself for details), renaming it to `settings.lgt`. Then, open the file in your favorite text editor and uncomment all the code snippets that you find relevant (e.g., to load essential tools at startup like `help`, `tutor`, `debugger`, `lgtdoc`, and `lgtunit`).

Speaking of favorite text editor, Logtalk provides support for several text editors and some IDEs. See the [`coding`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding/) directory for setup details.

Further advice on Logtalk setup can be found in the [`CUSTOMIZE.md`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/CUSTOMIZE.md) file.


## Application directory

Create a directory for your application (preferably outside of the Logtalk user directory, as this is updated when you update Logtalk) and copy the `loader-sample.lgt` (found at the root of the Logtalk distribution) to it renamed as `loader.lgt`. This source file will be the entry point for loading your application. See the comments in the file itself for guidance.

As testing is an essential part of developing an application, copy also the files `tester-sample.lgt` and `tests-sample.lgt` to the application directory and rename them, respectively, to `tester.lgt` and `tests.lgt`. The `tester.lgt` will be the entry point for running your application tests, defined themselves in the `tests.lgt` file. See the comments in the files themselves for guidance.
