---
layout: article
permalink: compatibility.html
title: Compatibility
---

Logtalk runs on any operating-system with a standards compliant modern
Prolog compiler. The interface between Logtalk and a specific backend
Prolog compiler is accomplished using a small adapter file. The Logtalk
distribution includes adapter files for all supported Prolog compilers:

-   [B-Prolog 8.1 or later versions](http://www.picat-lang.org/bprolog/)
-   [Ciao Prolog (version 1.21.0 or later)](http://ciao-lang.org) *(experimental)*
-   [CxProlog 0.98.1 or later versions](http://ctp.di.fct.unl.pt/~amd/cxprolog/)
-   [ECLiPSe 6.1\#143 or later versions](http://eclipseclp.org/)
-   [GNU Prolog 1.4.5 or later versions](http://www.gprolog.org/)
-   [JIProlog 4.1.7.1 or later versions](http://www.jiprolog.com/)
-   LVM 3.2.0 or later versions
-   [Quintus Prolog 3.3\~3.5](https://quintus.sics.se) *(experimental)*
-	[Scryer Prolog 0.9.0 or later versions](https://github.com/mthom/scryer-prolog) *(experimental)*
-   [SICStus Prolog 4.1.0 or later versions](https://sicstus.sics.se)
-   [SWI Prolog 6.6.0 or later versions](http://www.swi-prolog.org/)
-   [Tau Prolog (version 0.3.2 or later)](http://tau-prolog.org)
-   [Trealla Prolog (version 1.23.14 or later)](https://github.com/trealla-prolog/trealla) *(experimental)*
-   [XSB 3.8.0 or later versions](http://xsb.sourceforge.net/)
-   [YAP 6.3.4 or later versions](https://github.com/vscosta)

The *experimental* label means that some Logtalk features may not work as
expected due to the backend Prolog compilers being under development and
thus not stable and/or not (yet) providing required standard features.

Previous Logtalk 3.x versions and legacy 2.x versions provide support for
some other Prolog compilers, which are no longer supported due to lack of
compliance with official and de facto standards.
