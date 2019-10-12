---
layout: article
permalink: download.html
title: Download
aside:
  toc: true
---

**Latest stable version:** 3.30.0  
**Release date:** September 17, 2019

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
-   [YAP 6.3.4 or later versions](https://www.dcc.fc.up.pt/~vsc/yap/)

Legacy Logtalk versions (2.x) provide support for several other Prolog
compilers, which are no longer supported due to lack of compliance with
official and de facto standards.

Be sure to install the Prolog systems that you want to use as backend
compilers before installing Logtalk. In general, it is recommended that
you install the most recent versions of the Prolog systems.


## License

Logtalk is an open source programming language, distributed under the
[Apache License 2.0](https://github.com/LogtalkDotOrg/logtalk3/blob/master/LICENSE.txt).
The copyright notice and license applies to all files in this release
(including sources, documentation, and examples) unless otherwise
explicitly stated (see the [`NOTICE.txt`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/NOTICE.txt)
file for details on bundled third-party resources).


## Git repo

The Logtalk git repo is currently hosted at
[GitHub](http://github.com/LogtalkDotOrg/logtalk3).
Follow these [steps](running_developer_versions.html)
for running Logtalk development versions. See the
[release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
for the latest changes.

You may keep up to date on development changes by subscribing to the Logtalk commits [RSS
feed](https://github.com/LogtalkDotOrg/logtalk3/commits/master.atom).


## Sources

> [`logtalk-3.30.0.tar.bz2`](files/logtalk-3.30.0.tar.bz2)  
> `32ed6bf347ab96c7e15864275c2a931599a0864b0a0f63c3f837619085a16c62` (SHA-256)

Includes the HTML versions of the Handbook and the APIs documentation. The bundled 
[`INSTALL.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/INSTALL.md)
file contains manual installation instructions.


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
Logtalk on `/opt/local/share/` with integration scripts for supported
Prolog compilers on `/opt/local/bin`. Creates an `/Applications/Logtalk`
folder with links to the installed files.

> [`logtalk-3.30.0.pkg.zip`](files/logtalk-3.30.0.pkg.zip)  
> `65e42f8f48863d6f786ff4a6f7ab33e1f19bfbecb01163b7a089d51167187be1` (SHA-256)

A [MacPorts](http://www.macports.org/) portfile is also available. Users
may simply type the command `sudo port install logtalk` (or
`sudo port upgrade logtalk`) in order to install (or upgrade) Logtalk.
[Homebrew](http://mxcl.github.com/homebrew/) users may simply type the
command `brew install logtalk` (or `brew upgrade logtalk`) in order to
install (or upgrade) Logtalk. But do check first that the MacPorts
portfile and the Homebrew formula are up-to-date.


### Linux

Installs Logtalk on `/usr/local/share` with integration scripts for
supported Prolog compilers on `/usr/local/bin`.

> [`logtalk-3.30.0-1.noarch.rpm`](files/logtalk-3.30.0-1.noarch.rpm)  
> `58ae9eb00cbe4e0d3c3b28ef51b5d6ee024ef5d6bdec9405cb9e87cfb89eadd4` (SHA-256)

Package installation from the command-line is recommended:

```bash
$ sudo rpm -i logtalk-3.30.0-1.noarch.rpm
```


### Debian (e.g. Ubuntu)

Requires dpkg 1.15.0 or a later version. Installs Logtalk on
`/usr/share` with integration scripts for supported Prolog compilers on
`/usr/bin`.

> [`logtalk_3.30.0-1_all.deb`](files/logtalk_3.30.0-1_all.deb)  
> `6e7ad768f7af2466b9aec1c7529215cf4d80a0cbac3df9a7e47541e2e14cd67b` (SHA-256)

Package installation from the command-line is recommended:

```bash
$ sudo dpkg -i logtalk_3.30.0-1_all.deb
```


### Windows

Be sure to install a [compatible](#requirements) Prolog compiler
**before** running the Logtalk installer. Creates a `Logtalk` program
group in the `Start Menu` with integration shortcuts for supported
Prolog compilers and shortcuts for the accessing the Logtalk
documentation. Can be used by both admin and non-admin users.

> [`logtalk-3.30.0.exe`](files/logtalk-3.30.0.exe)  
> `b8dc9c3f331c211ed2372d01ab4efd791110b637242235f9c7fe091db987e6cc` (SHA-256)

Alternatively, on Windows 10 or Windows Server 2019, you can use the
Windows Subsystem for Linux (WSL) and install Logtalk using one of the
Linux installers listed above.

Automatically generated installers for the latest git version can be download from
[AppVeyor](https://ci.appveyor.com/project/pmoura/logtalk3/build/artifacts).


### SWI-Prolog pack

Logtalk is also available as a SWI-Prolog pack. The
[pack](http://www.swi-prolog.org/pack/list?p=logtalk) is handy for
*deployment* but not ideal for *development*, however, as all the
files in the distribution are buried in a relatively deep sub-directory.
The pack can be easily installed typing the query `pack_install(logtalk)`
at the top-level. Also available as a manual download.

> [`logtalk-3.30.0.tgz`](files/swi-prolog/packs/logtalk-3.30.0.tgz)  
> `c2cedf90149af366cac539a6763d7b32d9fe840bc26c3186fbb4bb51700c474e` (SHA-256)


### Arch Linux package

Logtalk is also available as an Arch Linux
[package](https://aur.archlinux.org/packages/logtalk/) contributed by
Ebrahim Azarisooreh.


## Documentation

HTML, ePub, PDF, and Texinfo versions of the Handbook (includes a tutorial, the User Manual, the Reference Manual, and the FAQ).
Note that the HTML version is **included** in the source and binary packages.

> [`logtalk-manuals-3.30.0.tgz`](files/logtalk-manuals-3.30.0.tgz)  
> `e727e31f795ce5469c7ba17e75288c1365ddfa296fa2417e0ef783980166400a` (SHA-256)


## Docker images

Nightly and stable Docker images are [available](https://hub.docker.com/u/logtalk/) using selected backend Prolog compilers.


## Older versions

Older releases are available [here](/files/) (but note that time stamps
do not match the release dates due to all the moving of these files
between servers along the years).


## Sponsorship

If you want to express you appreciation for Logtalk and help keep it a
sustainable project, your sponsorship is much appreciated. Sponsorship
monthly tiers can be browsed and selected by clicking in the `Sponsor`
button at the top of the page of the Logtalk [GitHub repo](http://github.com/LogtalkDotOrg/logtalk3).


## Registration

Consider [registering](regform.html) if you become a Logtalk user.
