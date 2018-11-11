---
layout: article
permalink: download.html
title: Download
aside:
  toc: true
---

**Latest stable version:** 3.21.0  
**Release date:** October 30, 2018

## Requirements

Logtalk runs on any operating-system with a standards compliant modern
Prolog compiler. The interface between Logtalk and a specific backend
Prolog compiler is accomplished using a small adapter file. The Logtalk
distribution includes adapter files for all supported Prolog compilers:

-   [B-Prolog 7.8 or later versions](http://www.picat-lang.org/bprolog/)
-   [CxProlog 0.98.1 or later versions](http://ctp.di.fct.unl.pt/~amd/cxprolog/)
-   [ECLiPSe 6.1\#143 or later versions](http://eclipseclp.org/)
-   [GNU Prolog 1.4.5 or later versions](http://www.gprolog.org/)
-   [JIProlog 4.1.6.1 or later versions](http://www.jiprolog.com/)
-   [Lean Prolog 4.5.7 or later versions](http://www.cse.unt.edu/~tarau/) *(experimental)*
-   [Qu-Prolog 9.7 or later versions](http://www.itee.uq.edu.au/~pjr/HomePages/QuPrologHome.html)
-   [Quintus Prolog 3.3\~3.5](https://quintus.sics.se) *(experimental)*
-   [SICStus Prolog 4.1.0 or later versions](https://sicstus.sics.se)
-   [SWI Prolog 6.6.0 or later versions](http://www.swi-prolog.org/)
-   [XSB 3.8.0 or later versions](http://xsb.sourceforge.net/)
-   [YAP 6.3.4 or later versions](http://www.dcc.fc.up.pt/~vsc/Yap/)

Legacy Logtalk versions (2.x) provide support for some other Prolog
compilers, which are no longer supported due to lack of compliance with
official and de facto standards.

Be sure to install the Prolog systems that you want to use as backend
compilers before installing Logtalk.


## License

Logtalk is an open source programming language, distributed under the
[Apache License 2.0](https://github.com/LogtalkDotOrg/logtalk3/blob/master/LICENSE.txt).
The copyright notice and license applies to all files in this release
(including sources, documentation, and examples) unless otherwise
explicitly stated.


## Git repo

The Logtalk git repo is currently hosted at
[GitHub](http://github.com/LogtalkDotOrg/logtalk3). You may keep up to
date on development changes by subscribing to the [Logtalk 3.x commits
RSS feed](https://github.com/LogtalkDotOrg/logtalk3/commits/master.atom).
Follow these [steps](https://github.com/LogtalkDotOrg/logtalk3/wiki/Running-Developer-Versions)
for running Logtalk development versions.

See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
for the latest changes. You may keep up to date on
development changes by subscribing to the Logtalk commits RSS [RSS
feed](https://github.com/LogtalkDotOrg/logtalk3/commits/master.atom).


## Sources

> [`logtalk-3.21.0.tar.bz2`](files/logtalk-3.21.0.tar.bz2)  
> `af28ccd307a53c7772caefc71c4d7e719a5aa83b3d07437c36eb8170fb2de97b` (SHA-256)


## Installers

Be sure to read the
[`README.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/README.md),
[`CUSTOMIZE.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/CUSTOMIZE.md), and
[`QUICK_START.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/QUICK_START.md)
files on the Logtalk user directory for important information, including
instructions on how to customize and run Logtalk. For Windows users,
this information is also available from the `Logtalk` program group in
the `Start Menu`.

The following installers are available for the latest version:


### macOS

Based on the [MacPorts](http://www.macports.org/) portfile. Installs
Logtalk on `/opt/local/share/` with integration scripts for selected
Prolog compilers on `/opt/local/bin`. Creates an `/Applications/Logtalk`
folder with links to the installed files.

> [`logtalk-3.21.0.pkg.zip`](files/logtalk-3.21.0.pkg.zip)  
> `f40307430042690f3c505051ee99f8dfb1cb5c4c52ea30ad986e00441afa2e69` (SHA-256)

A [MacPorts](http://www.macports.org/) portfile is also available. Users
may simply type the command `sudo port install logtalk` (or
`sudo port upgrade logtalk`) in order to install (or upgrade) Logtalk.
[Homebrew](http://mxcl.github.com/homebrew/) users may simply type the
command `brew install logtalk` (or `brew upgrade logtalk`) in order to
install (or upgrade) Logtalk. But do check first that the MacPorts
portfile and the Homebrew formula are up-to-date.


### Linux

Installs Logtalk on `/usr/local/share` with integration scripts for
selected Prolog compilers on `/usr/local/bin`. Package installation from
the command-line is recommended.

> [`logtalk-3.21.0-1.noarch.rpm`](files/logtalk-3.21.0-1.noarch.rpm)  
> `7754b964b40628c7d7a39f160999f40fef3a3b3c03d0c0e4c4d30b53b0dd5cc2` (SHA-256)


### Debian (e.g. Ubuntu)

Requires dpkg 1.15.0 or a later version. Installs Logtalk on
`/usr/share` with integration scripts for selected Prolog compilers on
`/usr/bin`. Package installation from the command-line is recommended.

> [`logtalk_3.21.0-1_all.deb`](files/logtalk_3.21.0-1_all.deb)  
> `e2b9bf60a1c15a6ed8d99c446902bcfec63f8cb67836935bd8ea0004ef9e6719` (SHA-256)


### Windows

Be sure to install a [compatible](#requirements) Prolog compiler
**before** running the Logtalk installer. Creates a `Logtalk` program
group in the `Start Menu` with integration shortcuts for supported
Prolog compilers and shortcuts for the accessing the Logtalk
documentation. Can be used by both admin and non-admin users.

> [`logtalk-3.21.0.exe`](files/logtalk-3.21.0.exe)  
> `1d11a3979228f1cb6e93da25c2fde643df787801ba48d3bbbfe36c7527508629` (SHA-256)


### SWI-Prolog pack

Logtalk is also available as a SWI-Prolog pack. The
[pack](http://www.swi-prolog.org/pack/list?p=logtalk) is handy for
*deployment* but not ideal for *development*, however, as the all the
files in the distribution are buried in a relatively deep sub-directory.
The pack can be easily installed typing the query `pack_install(logtalk)`
at the top-level. Also available as a manual download.

> [`logtalk-3.21.0.tgz`](files/swi-prolog/packs/logtalk-3.21.0.tgz)  
> `211f9654073aa0694f3b9358e05ca9e874b02235ac45ae67706bf561aa8d6930` (SHA-256)


### Arch Linux package

Logtalk is also available as an Arch Linux
[package](https://aur.archlinux.org/packages/logtalk/) contributed by
Ebrahim Azarisooreh.


## Documentation

HTML, ePub, and PDF versions of the Handbook (includes a tutorial, the User Manual, the Reference Manual, and the FAQ).
Note that the HTML version is **included** in the source and binary packages.

> [`logtalk-manuals-3.21.0.tgz`](files/logtalk-manuals-3.21.0.tgz)  
> `8b6d5e4a1bd7eff78d9d5ad40335ab14455a73436e31c3ceb18182bee40d53f0` (SHA-256)


## Docker images

Nightly and stable Docker images are [available](https://hub.docker.com/u/logtalk/) using selected backend Prolog compilers.


## Older versions

Older releases are available [here](/files/) (but note that time stamps
do not match the release dates due to all the moving of these files
between servers along the years).


## Registration

Consider [registering](regform.html) if you become a Logtalk user.
