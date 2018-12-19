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

This script performs a git clone and builds the sources archive, the manuals archive, the SWI-Prolog pack, and all the installers with the exception of the Windows installer.

To build the Windows `.exe` installer requires a PC or a virtual machine running Windows 7 or later and using the Inno Setup script that is also included with the distribution:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/windows](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/windows)

Build the Windows `.exe` installer first before running the
[`build_release.sh`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/build_release.sh)
script and copy the installer to the script directory.

The installers should be built and checked **before** tagging the stable
release in case some installer issue is found.

The HTML and SVG versions of the Handbook and the API documentation are usually kept
up-to-date using the scripts:

[https://github.com/LogtalkDotOrg/logtalk3/blob/master/manuals/sources/build_manuals.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/manuals/sources/build_manuals.sh)
[https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_html_docs.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_html_docs.sh)
[https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_svg_diagrams.sh](https://github.com/LogtalkDotOrg/logtalk3/blob/master/scripts/update_svg_diagrams.sh)

The HTML version requires [Sphinx](http://sphinx-doc.org/) with the
[Read the Docs theme](https://github.com/rtfd/sphinx_rtd_theme) installed.
Before running the scripts, the version data in the `conf.py` files must be updated.

After tagging the stable release (and pushing the tag to GitHub), the stable release Docker images are generated using the script at:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/docker](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/docker)

After uploading the generated archives, to update the SWI-Prolog pack, start `swipl` and use the following queries (replace `XY.Z` with the version numbers):

```logtalk
?- pack_remove(logtalk).    % if installed
...
?- pack_install('https://logtalk.org/files/swi-prolog/packs/logtalk-3.XY.Z.tgz').
...
```
