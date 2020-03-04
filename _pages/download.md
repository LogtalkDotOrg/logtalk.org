---
layout: article
permalink: download.html
title: Download
aside:
  toc: true
---

**Latest stable version:** 3.36.0  
**Release date:** March 3, 2020

<a class="github-button" href="https://github.com/sponsors/pmoura" data-icon="octicon-heart" aria-label="Sponsor @pmoura on GitHub">Sponsor</a>
<a class="github-button" href="https://github.com/LogtalkDotOrg/logtalk3" data-icon="octicon-star" aria-label="Star LogtalkDotOrg/logtalk3 on GitHub">Star</a>

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

> [`logtalk-3.36.0.tar.bz2`](files/logtalk-3.36.0.tar.bz2)  
> `ee31e8417d42bc09bbaedc82f7d142d79f13568cac30bcdc1eefccd2db44bc54` (SHA-256)

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

> [`logtalk-3.36.0.pkg.zip`](files/logtalk-3.36.0.pkg.zip)  
> `5dd43b50c5b34162ae3d7b8f3a8dbe140df074b8224f332001665624fe7344ce` (SHA-256)

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

> [`logtalk-3.36.0-1.noarch.rpm`](files/logtalk-3.36.0-1.noarch.rpm)  
> `c552dee4378fdc3d34ce3f14f31a694af012d42990ce57a32d1b790182acafe9` (SHA-256)

Package installation from the command-line is highly recommended:

```bash
$ sudo rpm -i logtalk-3.36.0-1.noarch.rpm
```

Logout and login after running the installer to activate the default values
for the Logtalk environment variables.


### Debian (e.g. Ubuntu)

Requires dpkg 1.15.0 or a later version. Installs Logtalk on
`/usr/share` with integration scripts for supported Prolog compilers on
`/usr/bin`.

> [`logtalk_3.36.0-1_all.deb`](files/logtalk_3.36.0-1_all.deb)  
> `3b65b59330678d2eb6e558f82b8379fbc5ec351e4fff3cf6f6ed1dfc96356033` (SHA-256)

Package installation from the command-line is highly recommended:

```bash
$ sudo dpkg -i logtalk_3.36.0-1_all.deb
```

Logout and login after running the installer to activate the default values
for the Logtalk environment variables.


### Windows

Be sure to install a [compatible](#requirements) Prolog compiler
**before** running the Logtalk installer. Creates a `Logtalk` program
group in the `Start Menu` with integration shortcuts for supported
Prolog compilers and shortcuts for the accessing the Logtalk
documentation. Can be used by both admin and non-admin users.

> [`logtalk-3.36.0.exe`](files/logtalk-3.36.0.exe)  
> `7937a208aa034461c805c3da8a892c15b04c6a66b7794387bcd9e602d07600d5` (SHA-256)  
> [VirusTotal scan results](https://www.virustotal.com/gui/url/3f2093ffb61369231608dee87731e10bcf04bbb7f7cdc86104963a49f51f27f3/detection)

Logtalk is also available as a [Chocolatey package](https://chocolatey.org/packages/logtalk/)
and can be installed or updated using the `choco install logtalk` and
`choco upgrade logtalk` commands. Alternatively, on Windows 10 or Windows
Server 2019, you can use the Windows Subsystem for Linux (WSL) and install
Logtalk using one of the Linux installers listed in this page.

Installing on Windows 10 requires temporarily turning off `Ransomware
protection` (in the `Windows Defender Security Center` preferences) if
enabled as the Logtalk installer creates the the Logtalk user directory
inside the `Documents` directory by default.

Automatically generated installers for the latest git versions can be download from
[AppVeyor](https://ci.appveyor.com/project/pmoura/logtalk3/build/artifacts).


### SWI-Prolog packs

Logtalk is also available as a SWI-Prolog pack. The
[pack](http://www.swi-prolog.org/pack/list?p=logtalk) is handy for *deployment*
but not ideal for *development*, however, as all the files in the distribution
(manuals, examples, ...) are buried in a relatively deep sub-directory.
The pack can be easily installed typing the query `pack_install(logtalk)`
at the top-level (use the `pack_info(logtalk)` query after installation
to find the installation directory). When upgrading an older pack, use
`pack_install(logtalk, [update(true)])` or simply `pack_remove(logtalk)`
followed by `pack_install(logtalk)`. See the pack specific
[`README.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/pack/logtalk/README.md)
file for details. Also available as a manual download:

> [`logtalk-3.36.0.tgz`](files/swi-prolog/packs/logtalk-3.36.0.tgz)  
> `617b3e3a8faa6e37263a54a17322b821effd7d90645f1b0d3a935b3a133522d1` (SHA-256)

In this case, change directory to the download directory, start SWI-Prolog,
and run the query `pack_install('logtalk-3.36.0.tgz').`

There's also an **experimental** pack that encapsulates de Logtalk
compiler and runtime in a `logtalk` module. See the pack specific
[`README.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/pack-experimental/logtalk/README.md)
file for details. This pack is only available as a manual download:

> [`logtalk-experimental-3.36.0.tgz`](files/swi-prolog/packs/logtalk-experimental-3.36.0.tgz)  
> `e671c7918cc2d1616a6892d913b68036ca8c917571ffd89390d4dede97d6956d` (SHA-256)

In this case, change directory to the download directory, start SWI-Prolog,
and run the query `pack_install('logtalk-experimental-3.36.0.tgz').`


### Arch Linux package

Logtalk is also available as an Arch Linux
[package](https://aur.archlinux.org/packages/logtalk/) contributed by
Ebrahim Azarisooreh.


## Documentation

HTML, ePub, PDF, and Texinfo versions of the Handbook (includes a tutorial, the User Manual, the Reference Manual, and the FAQ).
Note that the HTML version is **included** in the source and binary packages.

> [`logtalk-manuals-3.36.0.tgz`](files/logtalk-manuals-3.36.0.tgz)  
> `e53dd794d82cc77800ddd7c64b19d4867ccc6ef4d54c9cbf2192d351b9cb6454` (SHA-256)


## Docker images

Nightly and stable Docker images are [available](https://hub.docker.com/u/logtalk/) using selected backend Prolog compilers.


## Older versions

Older releases are available [here](/files/) (but note that time stamps
do not match the release dates due to all the moving of these files
between servers along the years).


## Sponsorship

If you want to express you appreciation for Logtalk and help keep it a
sustainable project, your [sponsorship](https://github.com/sponsors/pmoura)
is much appreciated. Sponsorship monthly tiers start at a symbolic $2 per
month to hopefully allow everyone to show their love and support for Logtalk.


## Registration

Consider [registering](regform.html) if you become a Logtalk user.

<script async defer src="https://buttons.github.io/buttons.js"></script>
