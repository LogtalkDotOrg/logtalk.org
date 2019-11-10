---
layout: article
permalink: testing.html
title: Testing
aside:
  toc: true
---

Several sets of unit tests are distributed with Logtalk. These include the tests in the `tests`, `tools`, `examples`, and `contributions` subdirectories. You can automate running these unit tests or your own unit tests by using the provided `scripts/logtalk_tester.sh` shell script.

Note that some tests require specific backend Prolog compiler features such as constraints, tabling, and threads. These tests are skipped when using backend Prolog compilers without native support for those features.

For information about the unit test framework and writing your own tests, see the [`lgtunit`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md)
tool documentation.

## Running unit tests on POSIX systems

In a POSIX system, you can run the provided unit tests by typing:

```shell
$ cd $LOGTALKUSER/tests/logtalk
$ logtalk_tester -p <back-end Prolog compiler>
...
$ cd ../../tools
$ logtalk_tester -p <back-end Prolog compiler>
...
$ cd ../examples
$ logtalk_tester -p <back-end Prolog compiler>
...
$ cd ../contributions
$ logtalk_tester -p <back-end Prolog compiler>
...
```

To run **all** tests distributed with Logtalk, type:

```shell
$ cd $LOGTALKUSER
$ logtalk_tester -p <back-end Prolog compiler>
```

If you didn't use one of the provided Logtalk installers or the installation script, you may need to type `logtalk_tester.sh` instead of just `logtalk_tester`.

The identifiers for the supported back-end Prolog compilers can be listed by typing:

```shell
$ logtalk_tester -h
...
```
 
Logtalk source code can be compiled in three different modes: _optimal_, _normal_, and _debug_. The `logtalk_tester` accepts an option, `-m`, to set the mode to be used to run the unit tests. Be aware, however, that running the unit tests in debug mode will be slower compared with the other two modes. Also, running the tests in optimal mode may flag errors not reported when running in normal mode due to e.g. the more extended use of static binding.

Note that, when running the unit tests using stable Logtalk releases, failed tests usually result from bugs in the backend Prolog compilers or from their lack of compliance with official and de facto standards. The most common issues are non-standard exception handling and syntax errors due to parser bugs. These issues can only be fixed by the developers of those Prolog compilers.

## Running unit tests on Windows systems

The `logtalk_tester.sh` script can also be used on Windows operating-systems by installing [Git for Windows](http://msysgit.github.io), which includes a bash shell implementation. After installation, you can start the bash shell by selecting `Git Bash` from the context menu. You will also need to add the `$LOGTALKHOME/scripts` and `$LOGTALKHOME/integration` directories plus the backend Prolog compiler executable directories to the system path environment variable. For example, assuming that you will be using YAP as backend Prolog compiler, the contents of your `~/.profile` file would contain something like:

```shell
# YAP
export PATH="/C/Program Files/Yap64/bin":$PATH
# Logtalk
export PATH="$LOGTALKHOME/scripts":"$LOGTALKHOME/integration":$PATH
```

When calling the scripts, you will need to use the `.sh` extension (e.g. use `yaplgt.sh` instead of simply `yaplgt`).

## Testing backend Prolog compilers

Starting with Logtalk 3.00.0-rc4, a set of unit tests for testing backend Prolog compilers for conformance with official and de facto standards is also provided. You can run them by typing:

```shell
$ cd $LOGTALKUSER/tests/prolog
$ logtalk_tester -p <back-end Prolog compiler>
...
```

Running these tests is advisable when developing portable Logtalk applications to ensure that all targeted backend Prolog compilers work as expected and that relevant differences between systems are accounted for. For more details about these tests see their [documentation](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tests/prolog/NOTES.md)

## Using a continuous integration server

The Logtalk unit test framework supports both TAP and xUnit output formats. Most CI servers support one or both formats for reporting and summarizing test results. In addition, the `logtalk_tester` automation script returns a non-zero exit value in case of failed tests, accepts user-defined arguments that are passed to application being tested, and traverses (by default) directories recursively looking for test sets to execute. See the script [man page](man/logtalk_tester.html) for details.

As an example, a CI server build script could contain:

```shell
# change directory to the test sets root directory
cd tests
# run all tests using the SWI-Prolog Logtalk pack, with results in TAP format, code
# coverage reports in XML format, and passing arguments foo, bar, and baz to the tests
logtalk_tester -p swipack -tap -c xml -- foo bar baz
```

By configuring the CI server TAP support to look for `tap_report.txt` files recursively inside the `tests` directory, the build report will summarize and list all the test results. By making the build script fail when the `logtalk_tester` script returns a non-zero value, the build will be marked as failed when there are failed tests. Consult your CI server documentation for details.

Most CI servers have HTML publishing plug-ins that should allow linking to the code coverage reports in the build page. But depending on the plug-in and on the web browsers used to view build results, you may need to convert the XML reports to HTML (instead of relying in the browser doing the conversion on the fly, which only works in some browsers) using a XSLT processor called as part of the build process. For example:

```shell
$ xsltproc -o coverage_report.html coverage_report.xml
```

## GitHub actions and workflows

GitHub actions and workflows for Logtalk and Prolog repos are available at:

[https://github.com/logtalk-actions](https://github.com/logtalk-actions)

These actions can be used for easily defining CI/CD workflows that use Logtalk and/or selected Prolog compilers.

## Caveats

Logtalk can act as a shared resource when doing concurrent builds. When two or more builds use the same Logtalk resources (e.g. library or tool files), a race condition may happen if the builds try to compile and load the same file. CI servers usually support, natively or using a plug-in, a way to throttle concurrent builds and/or the definition of locks for shared resources. A better solution, supported in Logtalk 3.11.0 and later versions, is to ensure that each Logtalk instance uses a unique scratch directory for temporary files. This requires a backend Prolog system supporting an initialization goal that is called, or an initialization file that is loaded, before Logtalk itself is loaded. Using SWI-Prolog as an example and assuming a POSIX system, add to its `.swiplrc` initialization file the following code:

```logtalk
:- multifile(logtalk_library_path/2).
:- dynamic(logtalk_library_path/2).

logtalk_library_path(scratch_directory, Directory) :-
    uuid:uuid(UUID),
    atom_concat('/tmp/', UUID, Directory).
```

Alternatively, start the Logtalk integration script for SWI-Prolog using the `-f` option to load the code from a file. For example:

```shell
$ swilgt -f "multiple_logtalk_instances_setup.pl"
```

A second example using GNU Prolog and assuming a POSIX system:

```logtalk
:- multifile(logtalk_library_path/2).
:- dynamic(logtalk_library_path/2).

logtalk_library_path(scratch_directory, Directory) :-
    temporary_name(lgtXXXXXX, Name),
    decompose_file_name(Name, _, Prefix, _),
    atom_concat('/tmp/', Prefix, Directory),
    make_directory(Directory).
```

You can add this code to a file, e.g. `multiple_logtalk_instances_setup.pl`, and then start Logtalk using:

```shell
$ gplgt --init-goal "consult(multiple_logtalk_instances_setup)"
```

Recent Logtalk versions include a [`parallel_logtalk_processes_setup.pl`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/library/parallel_logtalk_processes_setup.pl)
library file with sample setup code for selected backend Prolog compilers.
