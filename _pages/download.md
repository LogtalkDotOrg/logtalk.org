---
layout: article
permalink: download.html
title: Download
aside:
  toc: true
---

**Latest stable version:** 3.69.0  
**Release date:** August 21, 2023

<a class="github-button" href="https://github.com/sponsors/pmoura" data-icon="octicon-heart" aria-label="Sponsor @pmoura on GitHub">Sponsor</a>
<a class="github-button" href="https://github.com/LogtalkDotOrg/logtalk3" data-icon="octicon-star" aria-label="Star LogtalkDotOrg/logtalk3 on GitHub">Star</a>

## Requirements

Logtalk runs on any operating-system with a standards compliant modern
Prolog compiler. The interface between Logtalk and a specific backend
Prolog compiler is accomplished using a small
[adapter file](backend_requirements.html). The Logtalk distribution
includes adapter files for all supported Prolog compilers:

-   [B-Prolog 8.1 or later versions](http://www.picat-lang.org/bprolog/)
-   [Ciao Prolog (version 1.22.0 or later)](http://ciao-lang.org) *(experimental)*
-   [CxProlog 0.98.1 or later versions](http://ctp.di.fct.unl.pt/~amd/cxprolog/)
-   [ECLiPSe 6.1\#143 or later versions](http://eclipseclp.org/)
-   [GNU Prolog 1.4.5 or later versions](http://www.gprolog.org/)
-   [JIProlog 4.1.7.1 or later versions](http://www.jiprolog.com/)
-   [LVM 6.3.0 or later versions](https://permion.ai/)
-   [Quintus Prolog 3.3\~3.5](https://quintus.sics.se) *(experimental)*
-	[Scryer Prolog 0.9.1 or later versions](https://www.scryer.pl) *(experimental)*
-   [SICStus Prolog 4.1.0 or later versions](https://sicstus.sics.se)
-   [SWI Prolog 6.6.0 or later versions](http://www.swi-prolog.org/)
-   [Tau Prolog (version 0.3.2 or later)](http://tau-prolog.org)
-   [Trealla Prolog (version 2.18.7 or later)](https://github.com/trealla-prolog/trealla)
-   [XSB 3.8.0 or later versions](http://xsb.sourceforge.net/)
-   [YAP 6.3.4 or later versions](https://github.com/vscosta)

Be sure to install the Prolog systems that you want to use as backend
compilers before installing Logtalk. In general, it is recommended that
you install the most recent versions of the Prolog systems.

The *experimental* label means that some Logtalk features may not work as
expected due to the backend Prolog compilers being under development and
thus not stable and/or not (yet) providing required standard features. It
may also apply to legacy Prolog compilers.

Previous Logtalk 3.x versions and legacy 2.x versions provide support for
some other Prolog compilers, which are no longer supported due to lack of
compliance with official and de facto standards.


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

> [`logtalk-3.69.0.tar.bz2`](files/logtalk-3.69.0.tar.bz2)  
> `7828ac51372cd7eff7df3a8117a36dd53591583ce13191209db7e4ddee0ed424` (SHA-256)

Includes the HTML and Texinfo versions of the Handbook and the APIs documentation.
The bundled  [`INSTALL.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/INSTALL.md)
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

The following installers are available for the latest stable version:


### macOS

Installs Logtalk on `/opt/local/share/` with integration scripts for
supported Prolog compilers on `/opt/local/bin`. Creates an
`/Applications/Logtalk` folder with links to the installed files.

> [`logtalk-3.69.0.pkg.zip`](files/logtalk-3.69.0.pkg.zip)  
> `00acea81272d45c152c612b74069a70e250de8d2e4c7db68c2de14be87d21854` (SHA-256)

#### MacPorts

[MacPorts](https://www.macports.org/) users may use the command `sudo
port install logtalk` (or `sudo port upgrade logtalk`) in order to
install (or upgrade) Logtalk. Check first that the
[port](https://ports.macports.org/port/logtalk/) is up-to-date.

#### Homebrew

[Homebrew](https://brew.sh/) users may use the command `brew install
logtalk` (or `brew upgrade logtalk`) in order to install (or upgrade)
Logtalk. Check first that the [formula](https://formulae.brew.sh/formula/logtalk)
is up-to-date.


### Linux

Installs Logtalk on `/usr/local/share` with integration scripts for
supported Prolog compilers on `/usr/local/bin`.

> [`logtalk-3.69.0-1.noarch.rpm`](files/logtalk-3.69.0-1.noarch.rpm)  
> `55f41c999675a3cadfbe13915a4e7c8b601e0887e9acdf700606513f4a42e6f4` (SHA-256)

Package installation from the command-line is highly recommended:

```bash
$ sudo rpm -i logtalk-3.69.0-1.noarch.rpm
```

Logout and login after running the installer to activate the default values
for the Logtalk environment variables.


### Debian (e.g. Ubuntu)

Requires dpkg 1.15.0 or a later version. Installs Logtalk on
`/usr/share` with integration scripts for supported Prolog compilers on
`/usr/bin`.

> [`logtalk_3.69.0-1_all.deb`](files/logtalk_3.69.0-1_all.deb)  
> `33c2f9cbf0db034e189e397028bd8220c6a6876eeb9e28135f57de79fa9b808f` (SHA-256)

Package installation from the command-line is highly recommended:

```bash
$ sudo dpkg -i logtalk_3.69.0-1_all.deb
```

Logout and login after running the installer to activate the default values
for the Logtalk environment variables.


### Windows

Be sure to install a [compatible](#requirements) Prolog compiler
**before** running the Logtalk installer. Creates a `Logtalk` program
group in the `Start Menu` with integration shortcuts for supported
Prolog compilers and shortcuts for the accessing the Logtalk
documentation. Can be used by both admin and non-admin users.

[Installation video](https://www.youtube.com/watch?v=YE7ahXZibN4),
courtesy of [Paul Brown](https://pbrown.me/).

> [`logtalk-3.69.0.exe`](files/logtalk-3.69.0.exe)  
> `f4e7f3bf4c62eae4aa47be883822fefb1fb4b65679c10d5299d02ddaa0ec2fae` (SHA-256)  
> [VirusTotal scan results](https://www.virustotal.com/gui/url/b41d626cb0bca21f3d43df3e3f3e9a9c340d4a548126db2371d7a8747428c780)

Logtalk is also available as a [Chocolatey package](https://chocolatey.org/packages/logtalk/)
and can be installed or updated using the `choco install logtalk` and
`choco upgrade logtalk` commands. Alternatively, on Windows 10 or Windows
Server 2019, you can use the Windows Subsystem for Linux (WSL) and install
Logtalk using one of the Linux installers listed in this page.

Logtalk is also available as a [winget package](https://github.com/microsoft/winget-pkgs/tree/master/manifests/l/Logtalk/Logtalk),
thanks to the GitHub user [SpecterShell](https://github.com/SpecterShell),
and can be installed or updated using the `winget install logtalk` and
`winget upgrade logtalk` commands.

Installing on Windows 10 may require temporarily turning off `Ransomware
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

> [`logtalk-3.69.0.tgz`](files/swi-prolog/packs/logtalk-3.69.0.tgz)  
> `1d85800356342ce0d2a7287bd1ccad472a5b1859a835fe35b7f829fe4cda2e2c` (SHA-256)

In this case, change directory to the download directory, start SWI-Prolog,
and run the query `pack_install('logtalk-3.69.0.tgz').`

There's also an **experimental** pack that encapsulates de Logtalk
compiler and runtime in a `logtalk` module. See the pack specific
[`README.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/pack-experimental/logtalk/README.md)
file for details. This pack is only available as a manual download:

> [`logtalk-experimental-3.69.0.tgz`](files/swi-prolog/packs/logtalk-experimental-3.69.0.tgz)  
> `46c23172a7cd7d80832097e565516ed49f809c60dc0724f885a91a3b82c830aa` (SHA-256)

In this case, change directory to the download directory, start SWI-Prolog,
and run the query `pack_install('logtalk-experimental-3.69.0.tgz').`


### Arch Linux package

Logtalk is also available as an Arch Linux
[package](https://aur.archlinux.org/packages/logtalk/) contributed by
Ebrahim Azarisooreh.


## Documentation

HTML, ePub, PDF, and Texinfo versions of the Handbook (includes a tutorial, the User Manual, the Reference Manual, and the FAQ).
Note that the HTML and Texinfo versions are **included** in the source and binary packages.

> [`logtalk-manuals-3.69.0.tgz`](files/logtalk-manuals-3.69.0.tgz)  
> `85c505614269420251114578a8434ea89d8156a8f2a166339f4d7fdf349bbb99` (SHA-256)


## Docker images

Nightly and stable Docker images are [available](https://hub.docker.com/u/logtalk/) using selected backend Prolog compilers.


## Jupyter kernel

A Jupyter kernel is [available](https://pypi.org/project/logtalk-jupyter-kernel/) supporting Logtalk notebooks using selected backend Prolog compilers.
See e.g. [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/LogtalkDotOrg/notebooks/master) for an online example.

## Older versions

Older releases are available [here](/files/) (but note that time stamps
do not match the release dates due to all the moving of these files
between servers along the years).


## Sponsorship

If you want to express you appreciation for Logtalk and help keep it a
sustainable project, your [sponsorship](https://github.com/sponsors/pmoura)
is much appreciated. Both one time sponsorships and recurring sponsorships
are available, hopefully allow everyone to show their love and support for
Logtalk.


## Registration

Consider [registering](regform.html) if you become a Logtalk user.

<script async defer src="https://buttons.github.io/buttons.js"></script>
