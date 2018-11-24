---
layout: article
permalink: running_developer_versions.html
title: Running developer versions
aside:
  toc: true
---

Follow these steps to run a Logtalk developer version:

## Checking out the latest development version

From the command-line, type the following commands:

```shell
$ cd ~
$ git clone https://github.com/LogtalkDotOrg/logtalk3.git lgt3git
```

A `lgt3git` directory will be created on your home directory containing a local copy of the current Logtalk development version. Later, to update your local copy to the latest development version just type:

```shell
$ cd ~/lgt3git
$ git pull
```

In alternative, use one of several available GUI front-ends to `git`.

## Installing

### POSIX installation

If you use a bash shell, add the following lines to your `~/.profile` file:

```shell
LOGTALKHOME=$HOME/lgt3git
LOGTALKUSER=$HOME/lgt3git
PATH=$PATH:$LOGTALKHOME/tools/lgtdoc/xml:$LOGTALKHOME/scripts:$LOGTALKHOME/integration
MANPATH=$MANPATH:$LOGTALKHOME/man
export LOGTALKHOME LOGTALKUSER PATH MANPATH
```

If you use a csh shell, add the following line to your `~/.cshrc` file:

```shell
setenv LOGTALKHOME ${HOME}/lgt3git
setenv LOGTALKUSER ${HOME}/lgt3git
setenv PATH ${PATH}:${LOGTALKHOME}/tools/lgtdoc/xml:${LOGTALKHOME}/scripts:${LOGTALKHOME}/integration
setenv MANPATH ${MANPATH}:${LOGTALKHOME}/man
```

If your `lgt3git` directory is not in your home directory, adjust the paths above accordingly. Don't use relative paths such as `../` or `./` in the definition of the environment variables. Some Prolog compilers have trouble expanding environment variables, resulting in `file not found` errors when attempting to use the Logtalk integration scripts.

### Windows installation

Checkout the Logtalk development version into the directory `C:\lgt3git`. If you want to have Logtalk integration shortcuts for the supported Prolog compilers created, install [Inno Setup Unicode 5.3.0](http://www.jrsoftware.org/isinfo.php) (or a later version) and open the `C:\lgt3git\scripts\windows\logtalk.iss` file. Rebuild the Windows GUI installer and run it to install the Logtalk development version. In alternative, install a Bash shell such as the one provided by [Git for Windows](http://msysgit.github.io) and follow the steps above for the POSIX installation. 

## Running

### POSIX systems

You may run Logtalk by typing the name of the integration script with the `.sh` extension. For example, to run Logtalk using SWI-Prolog as the back-end compiler type `swilgt.sh`.

### Windows systems

Use the shortcuts available from the `Logtalk` program group in the `Start Menu`. Note that, depending on the chosen backend Prolog compiler, the first run of some shortcuts may need to be run as administrator.

## Customizing

See the file [`CUSTOMIZE.md`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/CUSTOMIZE.md) for tips on how to customize Logtalk.

## Switching between installed versions

If you want to run both stable and development versions of Logtalk on a POSIX system, you may instead keep the default values for the environment variables `LOGTALKHOME` and `LOGTALKUSER` and use the `logtalk_version_select` command to switch between installed versions. Simply perform a `git clone` of the Logtalk development version and install it by following the steps:

```shell
$ cd lgt3git/scripts
$ sudo ./install.sh
```

The `install.sh` shell script accepts an optional prefix and thus can also be used non-administrative users. For example:

```shell
$ cd lgt3git/scripts
$ ./install.sh -p $HOME
```

Logtalk development versions are identified by the name that will be used once they become the next released version. Thus, simply use the `logtalk_version_select` command to switch between versions. For example:

```shell
$ logtalk_version_select -l
Available versions: lgt2440 lgt2441 lgt3000a32 lgt3000a33
$ sudo logtalk_version_select lgt3000a33
Switched to version: lgt3000a33
```
