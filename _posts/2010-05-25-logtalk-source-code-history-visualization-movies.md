---
title: Logtalk source code history visualization movies
author: Paulo Moura
layout: article
tags:
  - development
  - visualization
show_edit_on_github: false
aside: false
---

Recently I came across two open-source tools for visualization of the commit history of source code: [codeswarm](http://code.google.com/p/codeswarm/) and [gource](http://code.google.com/p/gource/). Both tools support Subversion, the version control software currently used for Logtalk. Before that I used CVS. Unfortunately, the Logtalk Subversion repository only covers development from October 29, 2001 onwards (Logtalk 2.x development started on January, 1998). Even so, using the above tools provide interesting insight into the history of Logtalk for the past eight and a half years. The resulting videos are encoding using the MPEG-4 H264 video codec. I tried to upload the videos to YouTube but the apparently mandatory reconversion produced awful results.

The first video shows the Logtalk _code swarm_ between October 29, 2001 and May 4, 2010 (the date of the latest Logtalk stable release, version 2.39.2):

[https://logtalk.org/files/logtalk\_code\_swarm.mp4](https://logtalk.org/files/logtalk_code_swarm.mp4)

You will notice that the red color, representing commits related to the Prolog config files, often dominates. This is consequence of the lack of strong Prolog standards, which result in spending an inordinate amount of time working around portability issues.

The second video was produced by `gource` and covers the same time period:

[https://logtalk.org/files/logtalk_gource.mp4](https://logtalk.org/files/logtalk_gource.mp4)

This video excels at illustrating all aspects of Logtalk development work other than the Logtalk compiler/runtime itself. The "flashes" where the little green guy seems to touch most files happen when a new Logtalk version is released and I increment the version number in order to begin working on the next release.

A special thanks to the developers of the `codeswarm` and `gource` tools.
