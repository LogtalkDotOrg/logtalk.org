---
layout: article
permalink: releasing.html
title: Releasing new stable versions
aside:
  toc: true
---

The resources for releasing a new stable version are included in the
distribution:

[https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts)

See the [`NOTES.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/NOTES.md)
file in the directory for details. The main release script is:

[https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/build_release.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/build_release.sh)

This script performs a git clone and builds the sources archive, the manuals archive, the SWI-Prolog pack, and all the installers with the exception of the Windows installer. The macOS installer must be compressed from the Finder.

## Distribution files

The `BIBLIOGRAPHY.bib`, `CITATION.cff`, `VERSION.txt` should be update just before the new release is tagged. Same for the `core/core.pl` file, where the `'$lgt_version_data'/1` predicate definiton should have the status changed to `stable`. Any status version, e.g. `b04`, should also be removed from the `docs/sources/_conf.py` and `manuals/sources/conf.py` files. The `scripts/debian/changelog` file should be changed to reflect the released date and release week day.

## Windows installer

The build of the Windows `.exe` installer requires a PC or a virtual machine running Windows 7 or later and the Inno Setup script that is also included with the distribution:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/windows](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/windows)

Build the Windows `.exe` installer first before running the
[`build_release.sh`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/build_release.sh)
script and copy the installer to the script directory.

The installers should be built and checked **before** tagging the stable
release in case some installer issue is found.

The HTML and SVG versions of the Handbook and the API documentation are usually kept
up-to-date using the scripts:

- [https://github.com/LogtalkDotOrg/logtalk3/blob/master/manuals/sources/build_manuals.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/manuals/sources/build_manuals.sh)
- [https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_html_docs.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_html_docs.sh)
- [https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_svg_diagrams.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_svg_diagrams.sh)

The HTML version requires [Sphinx](http://sphinx-doc.org/) with the
[Read the Docs theme](https://github.com/rtfd/sphinx_rtd_theme) installed:

```bash
$ sudo pip install --upgrade pygments
$ sudo pip install --upgrade sphinx
$ sudo pip install --upgrade sphinx_rtd_theme
```

It may also be necessary to patch the Pygments installation with the latest version of syntax highlighting support files from the `coding/pygments` directory.

Before running the documentation scripts, the version data in the `manuals/sources/conf.py` and `docs/sources/_conf.py` files must be updated.

## Docker stable image

After tagging the stable release (and pushing the tag to GitHub), the stable release Docker images are generated using the script at:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/docker](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/docker)

## SWI-Prolog pack

After uploading the generated archives, to update the SWI-Prolog pack, start `swipl` and use the following queries (replace `XY.Z` with the version numbers):

```logtalk
?- pack_remove(logtalk).    % if installed
...
?- pack_install('https://logtalk.org/files/swi-prolog/packs/logtalk-3.XY.Z.tgz').
...
```

## Chocolatey package

The first step is to update the [LogtalkDotOrg/chocolatey-packages](https://github.com/LogtalkDotOrg/chocolatey-packages) repo `logtalk.nuspec` and `chocolateyInstall.ps1` files with the data for the new stable release, commit, and push the changes. Then, from a Windows system `cmd` shell, change directory to the repo clone and type the commands:

```text
git pull
choco pack
choco push -s https://push.chocolatey.org/
```

The above commands assume the API key is set. If that's not the case, before pushing a new release, the following command is required (with `KEY` replace by the actual key):

```
choco apikey --key KEY --source https://push.chocolatey.org/
```

## Updating HTML versions of the man pages

The HTML versions of the man pages are generated using [`roffit`](https://github.com/bagder/roffit) from the [https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_man_html_versions.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_man_html_versions.sh)
shell script. After running the script, the HTML files are saved in the same directory as the man pages.
