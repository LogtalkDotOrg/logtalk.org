---
title: ECLiPSe 6.x and singleton variables
author: Paulo Moura
layout: article
tags:
  - debugging
show_edit_on_github: false
aside: false
---

ECLiPSe 6.x, recently released, features an improved compiler, which, among other goodies, improves detection of singleton variables:

> Additional singleton warnings: The new compiler will detect additional cases of singleton variables, namely those that occur only once in a branch of a disjunction.

This may sound like a mandatory feature until you realize that most other Prolog compilers fail to detect such cases of singleton variables.
