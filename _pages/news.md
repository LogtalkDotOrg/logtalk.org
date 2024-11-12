---
layout: article
permalink: news.html
title: News
aside:
  toc: true
---

### 2024

##### November 12

> Logtalk 3.85.0 is now available for [downloading](download.html).
> This release adds a `linter` meta-flag to allow turning on/off all
> linter warnings; adds new `encodings` and `general` linter flags;
> converts some linter warnings into compilation errors; adds a new
> linter check for redundant entity qualification in predicate
> directives; changes the `logtalk_load_context/2` built-in predicate
> to type-check the key argument; improves error-checking for the
> `use_module/1-2`, `export/1`, and `reexport/2` directives; fixes
> a regression in the previous release that prevented reloading code
> after fixing compilation errors without restarting the current
> session; improves the documentation of the `issue_creator` tool;
> improves the Handbook sections on performance and meta-predicates;
> improves the Handbook documentation on the `logtalk_make/0-1`
> built-in predicates; updates the `meta_compiler` library to support
> optimization of meta-calls with closure meta-arguments that are
> messages to parametric objects; adds `diagrams` tool support for
> generating diagrams with local links to source file and directories
> that open in selected text editors; updates the `tutor` tool to
> explain additional compiler and developer tools warnings and errors;
> fixes harmless repeated warning in the `packs` tool when pack
> dependencies are not available; includes improvements and portability
> fixes to some examples; adds new tests and improves existing tests
> for Logtalk and standard Prolog features; and updates embedding scripts
> to accept an optional startup application goal argument. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 22

> Logtalk 3.84.0 is now available for [downloading](download.html).
> This release improves the compiler to detect and report recursive
> references to files and entities; fixes the compiler to prevent
> using grammar rules to try to redefine disjunction and conditional
> control constructs; improves the Handbook glossary; improves the
> documentation of the `logtalk_tester` script; improves the documentation
> of the `help`, `lgtdoc`, `packs` tools; adds new directory deletion
> predicates to the `os` library; improves the `hook_flows` library;
> includes improved documentation and additional tests for the
> `dictionaries` library; fixes `meta_compiler` library issues; adds
> `lgtunit` tool support for running just a selection of tests; adds
> `packs` tool support for installing and updating packs from local
> archives, for `gpg` encrypted pack and registry archives, for using
> `wget` in alternative to `curl`, and for for using `.sig` signature
> files in alternative to `.asc` signature files; adds `tutor` tool
> support for explaining selected `lgtunit`, `make`, and `packs` tool
> error messages; fixes the `dead_code_scanner` tool to avoid some false
> positives; fixes the `logtalk_tester` script to follow symbolic links
> when looking for test driver files; adds an example of defining a DSL
> for tests; adds additional tests for Prolog standard and de facto
> standard predicates; improves tests coverage for the `dead_code_scanner`
> and `packs` tools; and provides portability updates for SWI-Prolog and YAP.
> Thanks to Alex Kouznetsov, Michael McNally, and Lindsey Spratt for their
> contributions to this release. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 24

> Logtalk 3.83.0 is now available for [downloading](download.html).
> This release adds a new `consistency_error/3` built-in method;
> makes the compiler consistency errors more informative; provides
> linter fixes and improvements; fixes some compiler bugs, notably
> using a `uses/2` directive to change the order of predicate arguments
> to use it as a closure; improves the Handbook documentation of the
> `info/2` and `mode/2` directives; improves the Handbook documentation
> of the error handling built-in methods; improves the Handbook section
> on lambda expressions; updates the `lgtunit`, `help`, and `tutor`
> tools; adds additional tests for the Prolog standard logical update
> semantics and for several Prolog standard predicates; improves tests
> for Prolog standard control constructs and predicates; updates tests
> for linter flags; includes fixes for the SWI-Prolog based Docker
> image; and provides portability updates for XVM. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### August 20

> Logtalk 3.82.0 is now available for [downloading](download.html).
> This release adds support for runtime constructed messages for the
> built-in methods; fixes error handling for the `include/1` directive
> when dynamically creating new entities; includes changes, improvements,
> fixes, and tests for the linter tool; improves Handbook documentation
> of the message printing mechanism predicates; improves the `packs`
> tool handling of alternative pack dependencies; improves support for
> pack virtual environments; improves support for Allure test reports;
> includes additional tests for standard directives and predicates;
> and provides improvements and fixes for the portable Docker image.
> Thanks to Alex Kouznetsov and Paul Brown for the bug reports. For
> details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 16

> Logtalk 3.81.0 is now available for [downloading](download.html).
> This release updates the delegation control construct to also preserve
> the original meta-call context; adds support for runtime constructed
> `(^^)/2` goals; adds support for using the `(<<)/2` and `catch/3`
> control constructs in a grammar rule body; fixes meta-arguments
> handling issues (thanks to Alex Kouznetsov for the bug reports);
> accounts for the renaming of the LVM backend to XVM; improves
> documentation; improves the performance of the `json` library when
> parsing large files (thanks to Yurii Rashkovskii for the bug report);
> fixes the `meta_compiler` library expansion of meta-arguments that
> call Prolog module predicates; changes the `lgtunit` object `test/3`
> private predicate to no longer being declared as a meta-predicate,
> simplifying writing of meta-predicate tests; adds support for
> conditional and triggered breakpoints to the `debugger` tool;
> improves the `debugger` tool support for log points; improves the
> `debugger` tool performance when checking for leashed ports; fixes
> a bug in the `lgtdoc` tool when generating reStructuredText files;
> adds a new programming example illustrating the semantics of calling
> an inherited meta-predicate using a message to *self* versus using
> a *super* call; includes additional tests for the `(^^)/2` control
> construct; adds a Docker file for building an image with Logtalk,
> a subset of the supported Prolog backends, Jupyter, JupyterLab, and
> the Logtalk kernel; and includes new and improved VSCode/VSCodium
> support. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### June 4

> Logtalk 3.80.0 is now available for [downloading](download.html).
> This release changes the debugging API to allow multiple debug
> handlers to be loaded simultaneously; updates the compiler to
> support for using backend proprietary directives when dynamically
> creating objects and categories; updates the reflection API to
> better support developer tools; fixes a regression preventing
> linter warnings for duplicated clauses and grammar rules; fixes
> reporting of the number of compilation warnings that failed to
> count some of the warnings; fixes the `phrase/2-3` built-in
> methods to properly handle a runtime bound first argument when
> called from a meta-predicate (thanks to Alex Kouznetsov for the
> bug report); updates the documentation of the embedding scripts;
> adds ew `sequential_occurrences/2-3` list predicates to the `types`
> library; updates the `debugger` and `ports_profiler` tools for
> the new debug API; adds support for log points to the `debugger`
> tool; improves the `debugger` tool integration with other developer
> tools; improves the `packs` tool reporting when a pack is available
> from multiple registries; includes fixes for the `missing_data`
> example; includes new and improved VSCode/VSCodium support predicates;
> and provides portability updates for LVM and SWI-Prolog. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### May 15

> Logtalk 3.79.0 is now available for [downloading](download.html).
> This release fixes a regression in the `make` tool for the `check`
> target; fixes the term-expansion mechanism to allow generating
> multiple entity definitions; fixes left-recursion linter warnings for
> coinductive predicates; fixes the `code_metrics` tool implementation
> of the cyclomatic complexity and unique predicate nodes metrics to
> take into account multifile predicate definitions; fixes the `wrapper`
> tool reporting of missing `meta_predicate/1` directives; changes the
> `dead_code_scanner` and `lgtdoc` tools to print warnings using the
> same format used by the compiler; provides Handbook improvements; and
> includes new and improved VSCode/VSCodium support predicates. Thanks
> to Alex Kouznetsov for his bug reports and documentation feedback. For
> details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### May 6

> Logtalk 3.78.0 is now available for [downloading](download.html).
> This release improves the reflection API for better support code
> navigation features in IDEs and text editors; adds a new linter
> warning for left-recursion on clauses and grammar rules; includes
> documentation updates; fixes a portability issue in the
> `dead_code_scanner` tool; includes additional tests for Prolog
> standard predicates; adds support for VSCode and VSCodium code
> navigation features; and provides portability updates for SICStus
> Prolog and SWI-Prolog. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 2

> Logtalk 3.77.0 is now available for [downloading](download.html).
> This release updates the reflection API; adds linter warnings for
> `logtalk::print_message/3` goals; includes new and improved versions
> of the `code_metrics`, `diagrams`, and `packs` developer tools; adds
> and improves library and standard compliance tests; includes ePub
> and PDF versions of the APIs documentation; and provides portability
> updates for XSB. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### March 19

> Logtalk 3.76.0 is now available for [downloading](download.html). This
> release improves the reflection API; improves support for user-defined
> linter warnings; fixes some linter warnings for control constructs;
> fixes detection and reporting of attempts to declare category predicates
> or non-terminals as both multifile and dynamic; improves support for
> property-based testing, providing new arbitrary term generators and
> fixing issues with some shrinkers; includes a new and improved version of
> the `dead_code_scanner` tool; adds `packs` tools support for declaring
> operating-system dependencies in pack manifest files; updates the `packs`
> tool to clean the pack installation directory when restoring or
> (re)installing a pack from an archive; changes the `diagrams` and `lgtdoc`
> tool interpretation of options that exclude directories to also exclude all
> sub-directories; updates the `logtalk_tester.sh` script to allow it to be
> interrupted using Ctrl-C when the timeout option is used and to kill all
> created child processes on exit; fixes the `logtalk_tester.ps1` script
> reporting of broken test sets; fixes `dead_code_scanner` tool reported
> linter warnings in ports and contributions; improves and fixes several
> tests, notably when running on Windows; and provides portability updates
> for SICStus Prolog and XSB. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### February 27

> Logtalk 3.75.0 is now available for [downloading](download.html). This
> release improves the implementation of multi-threading features; adds 
> new random term generators to the `arbitrary` library and improves its
> documentation (joint work with Yurii Rashkovskii); adds new `os` library
> predicates for accessing operating-system data; updates the `lgtunit`
> tool to print both CPU time and wall time for tests; changed the `lgtunit`
> tool xUnit reports now use the tests wall time instead of CPU time; fixed
> a bug in the `packs` tool when specifying pack dependencies; improves the
> tests for the multi-threading examples; adds a test set for ISO Prolog
> standard logical update semantics; adds additional tests for the for the
> ISO Prolog standard `op/3` predicate; adds additional tests for the de
> facto Prolog standard `format/2-3` predicates; and includes portability
> updates for LVM, SICStus Prolog, and SWI-Prolog. For details and a complete
> list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 31

> Logtalk 3.74.0 is now available for [downloading](download.html). This
> release improves the linter warnings for unsound constructs in grammar
> rules and for if-then-else and soft-cut control constructs; improves
> the semantics and implementation of several multi-threading features;
> fixes compilation of `phrase/2-3` goals where the first argument is a
> `(::)/1-2` or `(^^)/2` control construct with a variable grammar rule
> body argument; fixes a regression where a compiler error when a source
> file term is not callable would be delegated to the backend; improves
> the Handbook documentation of several directives and built-in predicates;
> improves the Handbook documentation on dynamic predicates and grammar
> rules; adds a `listing` library (replacing the old undocumented one);
> adds a `recorded_database` library to help porting legacy Prolog code;
> fixes `json` library bugs; updates the `help` tool support to browse
> the Handbook and APIs documentation from the top-level; changes the
> default output directory for the `diagrams` tool to `./dot_dias`;
> updates the `tutor` tool for all recent linter updates; fixes a syntax
> error in the `logtalk_tester.ps1` script; improves the portability of
> the `fcube` port; updates the Advent of Code 2023 examples and several
> of the multi-threading examples; adds additional tests for the de facto
> standard `format/2-3` predicates and for the multi-threading built-in
> predicates; updates support for several text editors and syntax
> highlighters; updates the manual installation script to inform the user
> about the `INFOPATH` environment variable; fixes the Bash shell
> embedding scripts to actually use the default settings file when no
> `-s` option is passed; and includes portability updates for CxProlog,
> LVM, SICStus Prolog, SWI-Prolog, XSB, and YAP. Thanks to Yurii
> Rashkovskii for his bug reports and suggestions. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2023

##### December 12

> Logtalk 3.73.0 is now available for [downloading](download.html). This
> release adds linter warnings for deprecated arithmetic predicates and
> functions; adds warnings for comparing numbers using unification; adds
> support for using backend-declared deprecated built-in predicates in
> linter warnings; improves checking the availability of predicates in
> `user` for `uses/2` and `use_module/2` directives; avoids false positive
> linter warnings about non-terminals called as predicates when the
> caller is a phrase-like predicate declared in the backend adapter file;
> improves compiler reporting of term-expansion errors; fixes unknown and
> undefined predicate call warnings when the calls occur in an included
> file to report the actual location instead of the main file; fixes
> printing of grammar rules linter warnings to respect the `grammar_rules`
> flag; adds adapter files support for deprecated built-in predicates and
> for declaring phrase-like predicates that call non-terminals; improves
> the Handbook grammar section now uses W3C-style EBNF syntax compatible
> with the [Railroad Diagram Generator](https://www.bottlecaps.de/rr/ui),
> also fixing typos and omissions; improves the Handbook section on
> parametric objects; improves the documentation of the `wrapper` tool;
> adds an experimental `mutations` library for generating random mutations
> of terms of selected types (intended for eventual fuzz testing support);
> adds a `tsv` library for reading and writing TSV files; adds new predicates
> and non-terminals to the `types`, `grammars`, and `random` libraries;
> improves the performance of the `term_io` library predicates; includes
> updates and fixes to the `lgtunit`, `tutor`, and `wrapper` tools; fixes
> the PowerShell documentation scripts to avoid an error when converting
> XML files; improves the `logtalk_tester` scripts detection and reporting
> of broken test sets due to backend bugs; adds new `haunted_wasteland`,
> `scratchcards`, and `trebuchet` examples (solving Advent of Code 2023
> problems); adds new tests, updates, and fixes issues with the `poem`,
> `profiling`, `self_vs_this`, `errors`, `bench`, and `benchmarks` examples;
> adds additional tests for the `phrase/2-3` built-in methods and fixes
> an issue with a `setof/3` built-in method test; improves the macOS
> installer; fixes the `logtalk_user_setup.ps1` PowerShell script to use
> a valid path for the backup directory; and includes portability updates
> for B-Prolog, CxProlog, ECLiPSe, LVM, and SWI-Prolog. Thanks to Domingo
> Alvarez Duarte and Yurii Rashkovskii for their contributions to this
> release. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### November 9

> Logtalk 3.72.0 is now available for [downloading](download.html). This
> release improves compiler performance of source files defining objects
> and categories with a large number of facts; improves compiler performance
> when compiling ground terms; simplifies handling of plain Prolog terms
> when compiling source files; adds linter warnings for unsound calls in
> grammar rules; adds additional linter warnings for deprecated predicates;
> fixes a compiler error reporting issue; improves the Handbook section on
> performance; improves the Handbook documentation of some built-in methods;
> adds `lgtunit` documentation on mocking, testing and suppressing tests
> output, and measuring test execution times and memory usage; fixes the
> Handbook and APIs documentation search support to work offline; updates
> the `help`, `packs`, and `tutor` tools; improves the macOS installer;
> and updates the Windows installer for upcoming SICStus Prolog 4.9.x
> versions. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 12

> Logtalk 3.71.0 is now available for [downloading](download.html). This
> release removes support for Scryer Prolog; fixes compatibility with
> GNU Prolog versions older than 1.6.0; simplifies finding the goal to
> use to load an entity when browsing the APIs documentation; improves
> the documentation of embedding scripts; fixes a Texinfo navigation
> issue between Handbook and APIs documentation; updates automated
> testing to include any additional information from the Prolog backend
> `version_data` flag; updates the `debugger` tool to print a procedure
> box port for spy points when the port is unleashed; includes fixes and
> improvements to the `packs` tool linting of pack specifications;
> updates the `tutor` tool for the new linter warning on missing arithmetic
> functions; updates the `lgtdoc` tool to include the goal required for
> loading an entity in the entity documentation; and updates the `errors`
> and `document_converter` examples. For details and a complete list of
> changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 18

> Logtalk 3.70.0 is now available for [downloading](download.html). This
> release adds a new linter warning for missing arithmetic functions; fixes
> the GNU Prolog integration script when using the `--quiet` option; improves
> the documentation of the embedding scripts; fixes a Handbook code rendering
> issue; adds additional tests for the `java` library; provides improvements
> and fixes for the `packs` tool; updates the `logtalk_allure_report` scripts
> to support generating single file reports; improves and fixes the embedding
> scripts handling of the settings option; updates the `document_converter`
> example for faster conversion of large PDF files; and adds additional Unicode
> tests for the standard `sub_atom/5` predicate. For details and a complete
> list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### August 21

> Logtalk 3.69.0 is now available for [downloading](download.html). This
> release fixes the compilation of `read_term/2-3` and `write_term/2-3`
> goals when defining local operators; improves the documentation of
> directives, built-in methods, libraries, and tools; adds new experimental
> predicates to the `os` library for accessing full and read-only devices;
> improves the `lgtunit` tool support for flaky tests; fixes the `lgtunit`
> tool xUnit reports escaping of XML special characters, fixes the `diagrams`
> tool generation of SVG diagrams to avoid frequent Graphviz crashes; improves
> the `lgtdoc` tool support for documenting libraries where source files are
> organized in multiple sub-directories; improves the `tutor` tool explanations
> for some message sending warnings; adds additional tests for the `op/3`
> directive; updates the `document_converter` example to allow converting
> large files; and provides portability updates for LVM. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 28

> Logtalk 3.68.0 is now available for [downloading](download.html). This
> release adds a new `logtalk_load_context/2` predicate key for easy
> access to the entity (being compiled) relations (joint work with Yurii
> Rashkovskii); includes improved embedding scripts; improves `lgtunit`
> reporting of tests execution times; provides fixes and improvements to
> the `packs` tool; simplifies the Java examples setup scripts; includes
> new tests for Prolog standard syntax and built-in predicates; and
> provides portability updates for GNU Prolog, LVM, and SWI-Prolog. For
> details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 4

> Logtalk 3.67.0 is now available for [downloading](download.html). This
> release adds two new linter flags; abstracts how the linter and make
> tools check if a module defines a predicate; provides Handbook plus
> libraries and tools documentation updates; includes fixes and improvements
> for the `arbitrary` and `type` libraries handling of Unicode code
> points; adds new predicates to the `lgtdoc` tool; adds a new option
> to the `packs` tool `packs::update/2-3` predicates; adds `lgtunit` tool
> support for detecting and reporting discrepancies between the number of
> tests run and the total number of tests defined in a test set; adds
> `logtalk_tester` scripts support for using a GNU Prolog executable that
> includes Logtalk for better performance; adds `help` tool support for
> additional operating-systems; fixes bugs in the `debugger`, `diagrams`,
> `lgtdoc`, and `lgtunit` tools; updates several examples tests to use
> explicit assertions; adds new tests for Prolog standards directives and
> built-in predicates; improves tests for Prolog Unicode support; and
> provides portability updates for GNU Prolog, JIProlog, LVM, Scryer Prolog,
> and, Trealla Prolog. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### May 30

> Logtalk 3.66.0 is now available for [downloading](download.html). This
> release adds new keys to the `logtalk_load_context/2` built-in predicate
> for use with the term-expansion mechanism; adds two new meta-messages to
> the message printing mechanism to support user-defined printing goals;
> adds new linter warnings for DCGs, lambda expressions, predicate
> directives and backends without a module system; improves reporting of
> warnings when compiling auxiliary predicates; improves the Handbook and
> the documentation of several libraries and tools; adds a new `ulid`
> library for generating Universally Unique Lexicographically Sortable
> Identifiers; provides improvements and fixes to several tools, libraries
> examples, and contributions; adds additional compliance tests for Prolog
> standard predicates; fixes a registry issue when running the Windows
> installer; and provides portability updates for LVM, Quintus Prolog,
> Scryer Prolog, and, Trealla Prolog. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 27

> Logtalk 3.65.0 is now available for [downloading](download.html). This release
> documents the no longer experimental `(@)/1` control construct; adds a new
> `since` key to the `info/2` directive; adds two new values for the number of
> proofs to the `mode/2` directive; improves the Handbook sections on debugging
> and documenting predicates; reduces the number of atoms created by some tools
> and libraries; fixes the `git` library when working with paths containing
> spaces; includes significant fixes and improvements to the `debugger` and
> `lgtunit` tools; improves tests reporting; includes fixes for the Java
> examples and testing automation on Windows; adds notes for most of the
> skipped tests; includes new and revised tests; and provides portability
> updates for LVM, Scryer Prolog, and, Trealla Prolog. For details and a
> complete list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### March 28

> Logtalk 3.64.0 is now available for [downloading](download.html). This release
> fixes handling of `dynamic/1` directives for predicates with no clauses in 
> included files from dynamically created objects; fixes a performance issue where
> the compiler would not inline predicate definitions when the clause body goal
> uses parameter variables; improves the `csv` library error-checking; adds new
> predicates to the `java` library; includes changes for running all the Java-based
> examples on Windows; adds a `neo4j` example of using the `java` library to
> interface with Neo4j; adds new usability predicates to the `packs` tools; changes
> semantics of the `lgtunit` tool `clean_file/1` utility predicate to simplify
> usage; fixes the `logtalk_tester` scripts passing of calling options to sourced
> `tester` scripts in the test set directories; updates all tool PowerShell scripts
> to require version 7.3 or later; adds additional tests for Prolog standard
> meta-predicates; and includes portability updates for LVM. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### February 27

> Logtalk 3.63.0 is now available for [downloading](download.html). This release
> fixes linter warnings for unknown calls and suspicious calls to avoid false
> positives; fixes a compiler optimization bug for messages sent by an object
> to itself; adds a Handbook section on compiler formatting of errors, warnings,
> and comments; improves the documentation of the `random` library; adds GNU
> Prolog (1.5.1 or later) support for the `help` tool experimental features;
> improves the `diagrams` tool performance when generating library dependency
> diagrams; fixes and improves the `logtalk_tester.sh` script handling of the
> option to exclude directories; provides a new parametric objects example;
> adds additional tests for the Prolog `format/2-3` and `setup_call_cleanup/3`
> predicates; and updates syntax completion support for jEdit, Sublime Text,
> TextMate, and Vim. Thanks to Didier Garcin, Paul Brown, Jonathon Doran, and
> Lindsey Spratt for their contributions to this release. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 31

> Logtalk 3.62.0 is now available for [downloading](download.html). This release
> adds a new `tab(Expression)` message token to use with the message printing
> mechanism; simplifies the integration script for Trealla Prolog; updates the
> man pages for the integration scripts; adds an option to the `logtalk_tester`
> scripts for excluding directories; adds new `debugger` tool port commands;
> fixes a `debugger` tool issue with an automatic creep when returning to the
> port after user input; adds `lgtenv` scripts for creating packs virtual
> environments; adds new `packs` tool predicates and predicate options; updates
> the `diagrams` tool `lgt2svg` scripts to alert the user when one or more files
> cannot be converted; and adds additional tests for the Prolog `sub_atom/5`,
> `unify_with_occurs_check/2`, and `format/2-3` predicates (with contributions
> by Lindsey Spratt and Andrew Davison). For details and a complete list of
> changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2022

##### December 20

> Logtalk 3.61.0 is now available for [downloading](download.html). This release
> provides updated for several Prolog backend adapters and integration scripts
> for use in the [Jupyter kernel for Logtalk](https://github.com/LogtalkDotOrg/logtalk-jupyter-kernel);
> adds a new `ids` library for generating identifiers (Base64 encoded) with
> parametrizable text representation and number of bytes of randomness; adds
> new `pairs` library object predicates; adds `packs` tool support for using
> `git archive` for installing packs, providing a better user experience when
> the packs registry server uses Single Sign-On (SSO) for authentication; and
> includes additional tests for library predicates and standard arithmetic
> functions. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### November 15

> Logtalk 3.60.0 is now available for [downloading](download.html). This release
> adds a new linter check for the availability of predicates (and non-terminals)
> listed in `uses/2` and `use_module/2` directives; improves the readability of
> default flag values printed at startup; updates all backend adapter files to
> recognize `.pro` as a valid Prolog file name extension; includes Handbook,
> library, and tools documentation improvements; updates the manual installation
> instructions for `zsh` users; adds `json` library support for customizing the
> term representation of JSON objects and JSON pairs; adds new
> `reader::line_to_chars/2-3` library predicates; adds new and improved linter
> checks to the `lgtdoc` tool; adds a new `lgtunit` tool `file_path/2` predicate;
> includes fixes for the `logtalk_doclet` and `logtalk_tester` scripts; includes
> additional tests for several Prolog standard predicates; updated the
> `logtalk_user_setup` scripts to prevent misuse; and adds support for escape
> sequences inside double-quoted terms to most text editors and syntax highlighters.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 18

> Logtalk 3.59.0 is now available for [downloading](download.html). This release
> adds a new linter warning for naked meta-variables; adds linter warnings to
> the `lgtdoc` tool; updates the Bash shell integration scripts to be aware of
> the default Homebrew installation directory on macOS; updates all PowerShell
> scripts to check for a compatible PowerShell version; improves several Handbook
> sections; improves the documentation of the `random` and `types` libraries;
> includes fixes for the `logtalk_tester.ps1` script; updates the `lgtunit` tool
> to print a warning on invalid test options; fixes `lgtdoc` issues; updates and
> adds new Prolog standards compliance tests; adds new library predicates; and
> includes portability updates for Ciao Prolog and SICStus Prolog. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 27

> Logtalk 3.58.0 is now available for [downloading](download.html). This release
> adds a new linter warning for non-terminals called as predicates; adds a
> compilation warning when compiling a `logtalk_load_context/2` goal with an
> invalid key; fixes the compiler to not throw an instantiation error when the
> body of a clause is a variable; improves documentation on third-party dependencies
> to build documentation final formats and to use the developer tools; improves
> Handbook, libraries, and tools documentation; provides fixes and improvements
> for the `os`, `types`, and `arbitrary` libraries; includes a new `lgtunit`
> version with improved QuickCheck support; adds experimental predicates to the
> `help` tool to browse and search inline at the top-level the Texinfo versions
> of the Handbook and APIs documentation; fixes a missing message tokenization 
> in the `packs` tool; adds new Net-Clause Language (NCL) examples; adds new
> compliance tests for standard Prolog predicates and operators; adds a port of
> FCube, a prover for intuitionistic propositional logic; adds Emacs code snippets,
> contributed by Paul Brown; provides an embedding script for Ciao Prolog and
> improves the documentation of the embedding scripts; provides a PowerShell
> script for building the Handbook; updates the release build script to include
> all final formats for the Handbook and APIs documentation in the generated
> archives and installers; and includes portability updates for LVM, Trealla
> Prolog, and YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 26

> Logtalk 3.57.0 is now available for [downloading](download.html). This release
> improves the linter tool with new and refined warnings; improves the compilation
> of Prolog modules as objects; refines compiler error reporting; improves support
> for making predicates listed in `uses/2` and `use_module/2` directives available
> as scoped predicates for the entities containing the directives; adds Handbook
> sections on documenting predicate exceptions and on ports and contributions
> distributed with Logtalk; improves Handbook sections on Prolog integration and
> migration; adds links from library APIs documentation to the Handbook library
> descriptions; adds a `genint` library supporting application global and object
> local named generators for increasing positive integers; updates the `gensym`
> library with support for both global and object local symbol generators; adds
> new predicates to the `types` and `statistics` libraries; includes fixes and
> improvements to the `csv` library; adds new parametric objects to the
> `hook_objects` library; fixes the `arbitrary` library implementation of
> shrinkers when passed terms of unexpected types; includes an improved `packs`
> tool with new predicates, refined semantics, and support for registries that
> require personal token authorizations for access; fixes `lgtdoc` generated
> Sphinx documentation cross-referencing between applications and Logtalk
> distribution libraries; improves `tutor` tool feedback on some common linter
> reports; fixes `diagrams` tool cases where files listed as excluded would still
> be included in generated diagrams; adds new tests for Logtalk and Prolog
> features; and includes portability updates for CxProlog, LVM, SICStus Prolog,
> SWI-Prolog, and XSB. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### June 9

> Logtalk 3.56.0 is now available for [downloading](download.html). This release
> adds linter warnings for source file names and for if-then-else and soft-cut
> control constructs; improves the linter warnings for `findall/3` goals; adds
> support for calls to the database and reflection built-in methods where the
> predicate argument is only bound at runtime and is listed in a `uses/2` or
> `use_module/2` directive; fixes cases where predicate name conflicts in
> directives would not be reported; improves `arbitrary` library performance
> for several types; fixes issues with the `arbitrary` library generation of
> Unicode code points; provides an improved QuickCheck implementation;
> improves the `lgtunit` tool code coverage report format to enable reporting
> all test object parameterizations and files; adds linter warnings for missing
> documentation directives to the `lgtdoc` tool; improves performance of the
> `diagrams` tool; improves the documentation of libraries and tools; adds
> new tests and improves existing tests for Prolog standards compliance; and
> includes portability updates Scryer Prolog, SICStus Prolog, and Tau Prolog.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 28

> Logtalk 3.55.0 is now available for [downloading](download.html). This release
> adds Windows PowerShell versions of the setup, integration, embedding, and
> tools Bash shell scripts (joint work with Hans N. Beck); includes new and
> improved Handbook sections; adds a library file for loading all installed
> packs; improves handling of file paths by the `diagrams`, `lgtdoc`, and
> `wrapper` tools; improves the documentation of the `issue_creator`, `lgtunit`,
> and `packs` tools; includes fixes and improvements for the `lgtdoc` scripts; 
> updates the `update_html_docs.sh` and `update_svg_diagrams.sh` scripts to
> optionally generate packs documentation and diagrams; updates the Windows
> installer to copy the PowerShell integration and setup scripts to the system
> directory; updates documentation of the Visual Studio Code text editor
> Logtalk plug-in; adds new tests for official and de facto standard Prolog
> features; and includes portability updates Scryer Prolog, Tau Prolog, and YAP.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### March 22

> Logtalk 3.54.0 is now available for [downloading](download.html). This release
> adds a new linter warning for `catch/3` goals; adds support to user-defined linter
> warning messages for suspicious calls; adds a new Handbook section on the logic
> and control built-in public methods; improves the Handbook documentation on the
> term-expansion mechanism; improves documentation on applying the developer tools
> to plain Prolog code; adds new `union_find` and `grammars` libraries; improves
> the `sets` library thanks to a contribution by Adrián Arroyo Calle; adds linter
> checks for `format/2-3` goals to the `format` library; adds new predicates to the
> `pairs` library; adds new types to the `arbitrary` and `types` libraries; adds
> a `lgtunit` tool linter check for the use of unification goals in test outcome
> assertions; improves the performance of the `ports_profiler` tool; includes new
> predicates and fixes for the `packs` tool; fixes `lgtdoc` tool issues with Sphinx
> output; improves and updates examples; adds new standards compliance sets; and
> includes portability updates for B-Prolog, Ciao Prolog, ECLiPSe, GNU Prolog, LVM,
> Scryer Prolog, Tau Prolog, Trealla Prolog, and YAP. For details and a complete
> list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 20

> Logtalk 3.53.0 is now available for [downloading](download.html). This release
> includes a new developer tool, `issue_creator`, for automatically creating bug
> report issues for failed tests in GitHub or GitLab servers; adds support for
> using object aliases in the message delegation control construct; adds a
> Handbook section on calling Prolog foreign predicates; includes documentation
> fixes and improvements; adds new predicates to the `options` library; fixes a
> bug in the `intervals` library; updates the `logtalk_tester` automation script
> to use the new `issue_creator` tool; includes improvements to the `packs` tool;
> updates the `metagol` port; adds new test sets and tests for Prolog standards
> compliance; updates support for a new version of the Visual Studio Code text
> editor Logtalk plug-in; and includes portability updates for Ciao Prolog, GNU
> Prolog, LVM, SICStus Prolog, SWI-Prolog, Trealla Prolog, and YAP. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2021

##### December 7

> Logtalk 3.52.0 is now available for [downloading](download.html). This release
> fixes compiler and linter issues; includes an improved version of the new `packs`
> tool, a portable and decentralized package manager; adds new `dif` and `format`
> abstraction libraries; updates the `hook_objects`, `os`, and `types` libraries;
> includes documentation updates to the Handbook, tools, man pages, and scripts;
> includes fixes and improvements for the `debugger`, `diagrams`, `lgtunit`, and
> `tutor` tools; updates several programming examples; provides additional Prolog
> standards compliance tests; provides additional Logtalk tests; and includes
> portability updates for GNU Prolog, LVM, Tau Prolog, Trealla Prolog, XSB, and YAP.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 26

> Logtalk 3.51.0 is now available for [downloading](download.html). This release
> includes a beta version of the new `packs` tool, a portable and decentralized
> package manager; provides new `lgtunit` test outcomes and new input/output
> testing predicates; improves the compilation of large test sets by generating
> more compact code; improves the generation of Allure testing reports to include
> crashed and broken test sets; includes improved man pages to the testing scripts;
> includes `lgtdoc` tool bug fixes; improves the `make` tool; includes new `csv`
> library predicates; updates the `os` library for some backends; improves some
> of the programming examples; includes additional tests for Prolog compliance;
> fixes a Windows installer bug with settings files; and includes portability
> updates for all backends, notably by providing implementations of the
> `atomic_concat/3` and `atomic_list_concat/2-3` predicates. Thanks to Paul Brown,
> Michael T. Richter, and Doug Kearns for their contributions to this release.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### August 31

> Logtalk 3.50.0 is now available for [downloading](download.html). This release
> focus on improved documentation, developer tools, and test suites. The Handbook
> includes improved sections on documenting and testing applications, directives,
> and multi-threaded features. The testing automation script have been updated
> with support for passing base URLs to generate reports that link to the tests
> source code. The documenting and diagrams includes more versatile helper scripts
> with new options. A significant number of new tests have been added to the Prolog
> standards compliance suite for better coverage. This release also includes fixes
> and updates to libraries and examples plus portability updates for JIProlog, LVM,
> and SICStus Prolog. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 27

> Logtalk 3.49.0 is now available for [downloading](download.html). This release
> focus on improved Windows support, providing several fixes and improvements for
> libraries, tools, examples, and tests. Notably, it's again possible to use the
> testing automation script on Windows. Related portability updates are provided
> for B-Prolog, CxProlog, ECLiPSe, GNU Prolog, SICStus Prolog, SWI-Prolog, XSB,
> and YAP. This release also includes improved support for running Logtalk concurrently
> with multiple backends, improved testing support for reporting skipped test sets,
> additional standards compliance tests, and documentation updates. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 6

> Logtalk 3.48.0 is now available for [downloading](download.html). This release
> provides out of the box support for running parallel Logtalk processes; updates
> support for Ciao Prolog, CxProlog, GNU Prolog, LVM, SWI-Prolog, and Trealla Prolog;
> adds new Handbook sections on running parallel processes and on different stages of
> the multi-pass compiler; improves several Handbook sections; improves documentation
> of the `lgtunit` tool; improves tests for the `cbor` and `random` libraries; updates
> the `logtalk_tester` script to print the run time in seconds for each test set;
> adds a new example contributed by Paul Brown on adding portable application GUIs
> using Tcl and Tk; improves tests for multiple examples; includes new and improve
> standards compliance tests; and improves support for the Sublime Text editor. For
> details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### June 1

> Logtalk 3.47.0 is now available for [downloading](download.html). This release
> updates support for LVM, Scryer Prolog, and Trealla Prolog; fixes some bugs in
> the `json` and `term_io` libraries; improves support for flaky tests; adds new
> utility predicates for testing; fixes a testing automation script reporting bug;
> updates several examples; and improves and adds new tests for Logtalk features,
> tools, and standards compliance. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### May 4

> Logtalk 3.46.0 is now available for [downloading](download.html). This release
> adds experimental support for Scryer Prolog; updates version requirements for
> Ciao Prolog, LVM, and Trealla Prolog; adds nested dictionaries and HTML libraries
> (joint work with Paul Brown); adds new predicates to the `dictionaries` and
> `types` libraries; fixes portability issues in the `csv` and `os` libraries;
> fixes issues in the `arbitrary`, `dictionaries`, and `os` libraries; adds support
> for reporting tests as flaky tests to the `lgtunit` tool; adds new `lgtunit` tool
> predicates for checking text output; improves testing automation support; fixes
> escaping of special XML characters in the xUnit formats; improves manual
> installation instructions for POSIX systems; adds a new test set for Unicode
> features; adds tests for UTF-16 surrogates to the `encodings` example; adds new
> tests for the `open/4` Prolog standard predicate; and includes portability
> updates for Ciao Prolog, LVM, Trella ProLog, and XSB. For details and a complete
> list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### March 23

> Logtalk 3.45.0 is now available for [downloading](download.html). This release
> adds Base64, CBOR, JSON, and UUID libraries; adds new predicates to the `reader`
> and `term_io` libraries; adds new types to the `arbitrary`, `types`, and `os`
> libraries; fixes portability issues in the `os` library; removes deprecated
> library loader files; adds SPDX short-form identifiers to most files; updates
> the `lgtunit` tool to report individual tests execution time; improves test
> results reporting; adds a new test set for unbounded integer arithmetic; and
> includes portability updates for ECLiPSe, GNU Prolog, LVM, SICStus Prolog,
> SWI-Prolog, Trella ProLog, YAP. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### February 3

> Logtalk 3.44.0 is now available for [downloading](download.html). This release
> features new and improved linter checks; adds a new Handbook nomenclature section
> on the differences between Logtalk and Prolog; adds new Handbook glossary entries;
> adds libraries for CSV files reading/writing, option handling, and term input/output
> from/to atoms, chars, and codes; improves existing libraries; provides fixes
> and improvements for several developer tools; adds a shell script for generating
> Allure reports from test results; adds support for exporting test result in the
> xUnit.net v2 XML format; improves exporting of results in the JUnit/xUnit format;
> includes new and improved programming examples; adds new examples to the ToyCHR port;
> adds tests sets for the de facto standard hyperbolic arithmetic functions; adds
> additional tests for several arithmetic functions; adds Windows installer
> experimental support for creating an integration shortcut for Tau Prolog;
> updates the macOS installer
> support for users of the `zsh` shell; removes support for Qu-Prolog and for the
> multi-threaded version of XSB; and includes portability updates for LVM,
> SICStus Prolog, SWI-Prolog, Tau Prolog, Trella ProLog, YAP. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2020

##### December 22

> Logtalk 3.43.0 is now available for [downloading](download.html). This release
> focus once again on improved testing support and improved test suites for both Logtalk
> features and Prolog standards compliance of supported backends. It also provides
> compiler improvements and bug fixes, provides experimental support for Trealla ProLog;
> updates support for LVM and Tau Prolog; improves the top-level shortcut for loading files;
> includes a new `git` library; adds new predicates to the `queues` library; provides portability
> fixes for the `os` library; provides new predicates, improvements, and fixes for the
> `lgtunit` tool; provides fixes for the `debugger` and `lgtdoc` tools; improves the
> portability of the `bench` and `metainterpreters` examples; provides UltiSnips support
> for the Vim text editor, kindly contributed by Paul Brown; and includes other
> portability updates for most of the supported backends. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 26

> Logtalk 3.42.0 is now available for [downloading](download.html). This release
> focus on improved testing support and improved test suites for both Logtalk
> features and Prolog standards compliance of supported backends. It also
> adds new `logtalk_load_context/2` predicate keys, generalizes the linter checks
> for tautologies and falsehoods, fixes a `make` tool bug when using the `include/1`
> directive, adds experimental support for LVM as a backend compiler, fixes
> embedding errors when using GNU Prolog, improves support for Tau Prolog,
> provides an improved `os` library with fixes for several backends, and includes
> other portability updates for most of the supported backends. For details and
> a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 1

> Logtalk 3.41.0 is now available for [downloading](download.html). This release
> adds new linter checks for tautologies and falsehoods, adds a new convenience
> error throwing built-in method for uninstantiation errors, provides updated
> support for Tau Prolog, provides library fixes for Quintus Prolog and SICStus
> Prolog, fixes Handbook ePub file validation errors with some readers, and
> includes new and improved Prolog standards compliance tests.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### July 29

> Logtalk 3.40.0 is now available for [downloading](download.html). This release
> adds support for module aliases, includes improvements for the documentation
> and the `doclet` and `lgtdoc` developer tools, adds new Prolog standards
> conformance tests, adds a new programming example illustrating the use of
> modules aliases, and provides updated support for Qu-Prolog and Tau Prolog.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### June 17

> Logtalk 3.39.0 is now available for [downloading](download.html). This release
> improves the linter checks for `is/2` goals, provides an experimental hook
> predicate enabling user-defined linter warnings, improves the `make` tool
> check of library aliases, adds experimental support for Ciao Prolog and Tau
> Prolog, drops Lean Prolog support due to unfixed bugs that prevent Logtalk
> startup, fixes broken Handbook links do API documentation, adds new predicates
> to the `coroutining` and `os` libraries, adds new type edge cases to the
> `arbitrary` category for use with property-based testing, adds a new hook
> object to the `hook_objects` library for suppressing goals in clauses,
> includes fixes and improvements for property-based testing, adds support for
> a `subsumes/2` outcome to the `test/2-3` test dialects, includes fixes and
> improvements for the test automation script, adds new unit tests, includes
> new examples of parametric objects programming idioms, and updates the Windows
> installer to also detect SICStus Prolog 4.6.x versions. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 28

> Logtalk 3.38.0 is now available for [downloading](download.html). This release
> adds a new lint check for non-tail recursive predicate definitions, improves
> the lint checks for deprecated predicates, includes fixes and improvements for
> the `arbitrary` library category, implements several new QuickCheck options,
> simplifies error handling and reporting for the QuickCheck predicates and test
> dialects, improves the documentation of several developer tools, improves the
> usability of the SVG diagrams generated by the `diagrams` tool by adding CSS
> support, and updates support for the Kate text editor. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 2

> Logtalk 3.37.0 is now available for [downloading](download.html). This release
> adds a new meta-message to the message printing mechanism, allows the `user`
> pseudo-object to be used as an event monitor, fixes a reflection API bug that
> could result in duplicated or redundant entity operator properties, improves
> support for compiling modules as objects, includes significant updates to the
> Handbook with new and improved sections, includes new and improved glossary
> entries, provides new library hook objects, adds and improves notes on applying
> the developer tools to Prolog codebases, improves the `lgtunit` tool automation
> support, adds a simple example of Aspect-Oriented Programming using hot patching
> and event-driven programming support, and provides updated support for SWI-Prolog
> and YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### March 3

> Logtalk 3.36.0 is now available for [downloading](download.html). This release
> adds lint checks for cyclic terms and float comparisons, improves the lint
> checks for unification goals that are always true or always false, changes the
> preferred format of dates and versions in `info/1` directives for ISO 8601
> standard compliance and support for upcoming version management tools, updates
> the list of directories searched for settings files, includes fixes and
> improvements for compiler and runtime error handling, includes Handbook and
> tools documentation improvements, adds a new `hook_objects` library providing
> convenient hook objects for defining custom expansion workflows, improves
> portability of several libraries for backends supporting rational numbers,
> improves the reliability of the `logtalk_tester` automation script and adds
> command-line options to pass additional options to the backend compiler and
> to set output verbosity, improves `tutor` tool warning explanations, adds
> tests for the definitions of the standard ISO Prolog operators, adds new
> introductory examples for key Logtalk semantics, adds a SWI-Prolog Pengines
> integration example (contributed by Michael T. Richter), updates code
> snippets for the supported text editors, and provides updated support for
> ECLiPSe, Qu-Prolog, and SWI-Prolog. For details and a complete list of changes,
> please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 30

> Logtalk 3.35.0 is now available for [downloading](download.html). This release
> adds a lint check for redefined standard operators, simplifies and improves
> the compilation and execution performance of meta-calls and lambda expressions,
> improves compilation of modules as objects for applying the developer tools,
> improves support for parameter variables in directives, fixes two optimization
> bugs in atypical code, adds library overviews to the handbook, adds new and
> improves existing handbook sections, improves library documentation, improves
> integration with SWI-Prolog graphical tracer and profiler tools (after
> feedback and support from Daniel Gross), updates the tutor tool for the
> latest lint warnings, improves test coverage of control constructs and
> directives, adds new didactic example definitions of meta-predicates,
> improves ctags support (contributed by Paul Brown), and provides updated
> support for ECLiPSe, SWI-Prolog, and YAP. For details and a complete list
> of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 7

> Logtalk 3.34.0 is now available for [downloading](download.html). This
> release adds support for defining predicate shorthands in `uses/2` and
> `use_module/2` directives, allows local operators to also be declared in
> scope directives to simplify compilation of included files, adds support
> for the legacy Prolog database built-in predicates that take a clause reference
> argument, improves detection of deprecated Prolog built-in predicates,
> improves compilation of modules as objects, includes a new and improved
> Handbook sections, improves `lgtunit` tool documentation and code coverage
> support, provides an updated `expecteds` library, includes new and updated
> tests for Prolog built-in predicates, includes new and updated programming
> examples, updates the Debian installer to define default values for the
> Logtalk environment variables, and provides updated support for ECLiPSe,
> SWI-Prolog, and YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2019

##### December 3

> Logtalk 3.33.0 is now available for [downloading](download.html). This
> release adds make tool support for detecting duplicated library aliases,
> fixes silent loading of settings files when used to load libraries and
> tools, updates the documenting tool to list inherited public predicates
> in entity API documentation, improves tool documentation, adds new library
> predicates, includes fixes and improvements for libraries and tools, adds
> new library tests, adds new multi-threading programming examples, adds an
> example of using the question-asking mechanism, fixes example issues, and
> provides updated support for ECLiPSe, SICStus Prolog, SWI-Prolog, XSB, and
> YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### November 5

> Logtalk 3.32.0 is now available for [downloading](download.html). This
> release adds support for multifile meta-predicates, improves some lint
> checks, includes fixes and improvements for embedding applications,
> includes documentation updates and improvements, adds support for
> storing settings files in the `$HOME/.config` directory, improves
> the `lgtunit` tool support for TAP and xUnit outputs, simplifies
> generation of API documentation in Sphinx format, fixes some bugs
> in the `diagrams` tool, adds tests for multifile meta-predicates and
> for the de facto standard arithmetic functions `gcd/2` and `sign/1`,
> adds sample implementations of the "many worlds" design pattern using
> inheritance and parametric solutions, adds a new example illustrating
> the question asking mechanism, and provides updated support for
> GNU Prolog, SICStus Prolog, SWI-Prolog, and YAP. For details and a
> complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 15

> Logtalk 3.31.0 is now available for [downloading](download.html). This
> release adds new and improved lint checks for control constructs and
> built-in predicates, adds support for using `encoding/1` directives in
> included files, improves support for compiling modules as objects,
> includes documentation updates and improvements, includes fixes and updates
> for the `code_metrics` and `lgtunit` tools, includes a port of ToyCHR,
> updates Textadept editor support, updates the Windows installer to
> support Chocolatey packages, and provides portability updates for
> ECLiPSe, GNU Prolog, SICStus Prolog, SWI-Prolog, and YAP. For details
> and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 17

> Logtalk 3.30.0 is now available for [downloading](download.html). This
> release adds new and improved lint checks, improves compilation of
> modules as objects, fixes documentation link issues, includes updated
> `debugger` and `tutor` tools, updates Textadept editor support, and
> provides portability updates for SICStus Prolog and SWI-Prolog.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 3

> Logtalk 3.29.0 is now available for [downloading](download.html). This
> release adds new and improved lint checks, adds a `duplicated_clauses`
> compiler flag, fixes a text encoding issue when using the `include/1`
> directive, adds a new Handbook section on the compiler multi-pass
> implementation, adds cross-links between Handbook and APIs documentation,
> includes an updated `tutor` tool, and provides portability updates for
> ECLiPSe, Qu-Prolog, SICStus Prolog, SWI-Prolog. For details and a complete
> list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### August 14

> Logtalk 3.28.0 is now available for [downloading](download.html). This
> release adds a new `tutor` learning tool for helping new users understand
> compiler warning and error messages, improves compiler lint checks, fixes
> reporting of singleton variables in included files, improves the Windows
> installer, provides a workaround for recent SWI-Prolog Windows installers
> no longer writing registry keys, adds an AppVeyor script to build and make
> available a Windows installer per commit, adds new unit tests, includes
> documentation updates and improvements, improves syntax coloring of escape
> sequences in quoted atoms and character code number notation, and provides
> portability updates for SWI-Prolog. For details and a complete list of
> changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### June 18

> Logtalk 3.27.0 is now available for [downloading](download.html). This
> release adds a `uses/1` directive for declaring object aliases, updates
> the `uses/2` and `use_module/2` directives to support using a parameter
> variable in place of the object or module identifier (thus allowing using
> implicit message sending and implicit module qualification with dynamic
> binding), adds a lint check for built-in predicates used as directives,
> improves navigation of APIs documentation, adds the documentation of the
> developer tools to the Handbook, adds support for generating Texinfo
> versions of the Handbook and the APIs documentation, reorganizes the
> libraries to simplify usage, adds unit tests for most of the libraries,
> includes fixes and improvements for libraries and developer tools, and
> provides portability updates for SWI-Prolog. For details and a complete
> list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### May 8

> Logtalk 3.26.0 is now available for [downloading](download.html). This
> release features a new version of the `diagrams` tool with significant
> improvements and includes a new `timeout` portability library, an updated
> Metagol port, and updated examples. For details and a complete
> list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### April 2

> Logtalk 3.25.0 is now available for [downloading](download.html). This
> release focus on compiler linter and QuickCheck improvements. It adds 15
> new linter checks, notably for possibly non-steadfast predicates, predicate
> and variable names that do not follow coding guidelines, repeat loops
> without a cut, redundant calls to built-in predicates and control constructs,
> cuts in clauses for multifile predicates, variable use in all-solutions
> predicate calls, and several others suspicious calls and constructs; adds
> two new compiler flags, `steadfastness` and `naming`, to control the
> corresponding linter warnings; improves the goal-expansion mechanism to
> prevent infinite loops when the goal to be expanded resulted from a
> previous expansion of the same goal; updates the `coinductive/1` directive
> to also accept non-terminal indicators; updates the Handbook glossary;
> improves the Handbook sections on performance and on calling Prolog
> meta-predicates; fixes issues in the PDF version of the Handbook;
> improves `lgtunit` tool support for QuickCheck by allowing the
> user to specify the maximum number of shrink operations and by testing
> edge cases first; adds definitions for new types that take as argument a
> character set; adds shrinking supporty for most of the types supported by
> the `arbitrary` category; adds support for defining type edge cases to the
> `arbitrary` category; improves shrinking of list types; fixes steadfastness
> issues with some library predicates; and provides portability updates for
> GNU Prolog, SICStus Prolog, SWI-Prolog, and YAP. For details and a complete
> list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### February 28

> Logtalk 3.24.0 is now available for [downloading](download.html). This
> release adds a `threaded_cancel/1` built-in predicate; includes compiler
> linter improvements; adds new handbook sections and includes several
> improvements to existing sections; new file/stream reader library; improves
> support for generating API documentation in Sphinx format; new tests; new
> examples of using futures and threading state; new support for the SubEthaEdit
> 4.x/5.x text editor; and portability updates for SWI-Prolog. For details and
> a complete list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### January 30

> Logtalk 3.23.0 is now available for [downloading](download.html). This
> release includes compiler and documentation improvements and fixes; new
> coroutining and list zipper libraries; improved expected and optional term
> libraries; a new `debug_messages` tool; improvements to the `lgtunit` tool;
> a port of the Metagol ILP system; new tests; new examples of serialization
> of objects, application of zippers, and application of expected terms;
> updated Windows installer for detecting the new SICStus Prolog 4.5.0
> version; and portability updates for SICStus Prolog and SWI-Prolog. For
> details and a complete list of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2018

##### December 18

> Logtalk 3.22.0 is now available for [downloading](download.html). This
> release provides new and improved handbook sections; improves the
> readability of PDF and HTML versions of the handbook and the APIs
> documentation; adds sample implementations of object-oriented behavioral,
> creational, and structural design patters; improves the sample embedding
> scripts; adds CodeMirror support; plus other improvements and fixes to
> the compiler, runtime, adapter files, documentation, library, tools,
> examples, and installation scripts. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### October 30

> Logtalk 3.21.0 is now available for [downloading](download.html). This
> release adds a contributor code of conduct; includes several improvements
> to the manuals; moves the manuals and the core, library, tools, and
> contributions APIs documentation to Sphinx using the Read the Docs theme;
> includes support for publishing user applications API documentation using
> Sphinx; improves support for hot patching; improves test automation support;
> updates and improves some of the examples; fixes a Windows shortcuts issue;
> plus other improvements and fixes to the documentation, library, tools,
> and coding support. For details and a complete list of changes, please
> consult the the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### September 5

> Logtalk 3.20.0 is now available for [downloading](download.html). This
> release adds a set of entry level examples, improves lint checks for
> missing meta-predicate directives, improves support for lambda
> expressions in grammar rules, fixes some optimization bugs, improves
> library type-checking support, adds new library random and set
> predicates, improves performance of the Java interface library, plus
> other improvements and fixes to the documentation, compiler, library,
> and tools. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

##### August 1

> Logtalk 3.19.0 is now available for [downloading](download.html). This
> release removes all deprecated Logtalk 2.x features; improves the
> reference manual; adds new library predicates for number comparison;
> adds new ramdom library predicates; adds cyclomatic complexity and
> number of entity rules code metrics; improves existing code metrics;
> adds new Prolog standard compliance tests; adds new tests for built-in
> methods and for the new library predicates; adds new examples; adds
> support for the highlight.js syntax highlighter and updates support
> for most text editors and syntax highlighters; provides portability
> updates for ECLiPSe, GNU Prolog, Lean Prolog, Qu-Prolog, Quintus
> Prolog, SWI-Prolog, and XSB; plus other improvements and fixes to the
> documentation, compiler, library, and tools. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 26

> Logtalk 3.18.0 is now available for [downloading](download.html). This
> release adds a new lint checks for detecting suspicious calls and a
> compiler flag, `suspicious_calls/1`, to control printing of suspicious
> call warnings, which now also print the recommended alternative call;
> improves the performance of creating dynamic entities; fixes a bug
> that prevented inlining of linking clauses that call Prolog module
> predicates; improves reporting of singleton variables when using
> parameter variables; updates the contributing guidelines, moving from
> the Contribution License Agreement (CLA) to the more developer
> friendly Developer Certificate of Origin (DCO); adds a port of Peter
> Van Roy EDCGs implementation; adds an experimental Halstead complexity
> metric to the `code_metrics` tool; adds new Prolog standards
> compliance tests; adds examples of using EDCGs, optional terms, and
> expected terms; provides portability updates for JIProlog, SICStus
> Prolog, and SWI-Prolog; plus other improvements and fixes to the
> documentation, compiler, library, tools, and examples. For details and
> a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 21

> Logtalk 3.17.0 is now available for [downloading](download.html). This
> release improves dynamic binding performance; adds a new lint flag for
> detecting suspicious calls; adds a new make target for helping
> benchmarking performance; fixes a multi-threading regression bug;
> includes improvements and fixes to some of the examples; improves the
> bundled scripts; provides portability updates for SWI-Prolog and YAP;
> plus other improvements and fixes to the documentation, compiler,
> library, tools, examples, and installers. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April 30

> Updated backend Prolog compilers [benchmarks](performance.html) page.

#### April 24

> Logtalk 3.16.0 is now available for [downloading](download.html). This
> release improves support for embedding Logtalk and Logtalk
> applications, including in saved states and executables; adds new lint
> flags for more fine-grained control of compiler warnings; changes all
> exception context arguments for runtime errors to always including the
> execution context, thus providing extended information in case of
> error; compiles calls to most Logtalk built-in predicates to improve
> compile time type-checking when the arguments are sufficiently
> instantiated and to return the actual execution context in case of
> runtime error; improves the embedding helper scripts for selected
> backend compilers; adds new type definitions; adds sample
> configuration setup for running parallel Logtalk processes for
> selected backend compilers; includes new and improved unit tests;
> provides portability updates for ECLiPSe, GNU Prolog, Lean Prolog, and
> SICStus Prolog; plus other improvements and fixes to the
> documentation, compiler, library, tools, examples, and installers. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 21

> Logtalk 3.15.0 is now available for [downloading](download.html). This
> release improves runtime performance when using static binding;
> features new and improved compiler lint checks for duplicated
> directives; adds embedding helper scripts for selected backend
> compilers; adds new type definitions; adds new utility predicates for
> unit testing; improves support for QuickCheck; adds support for URL
> links in code coverage reports; adds support for predicate
> cross-referencing diagrams with URL links from predicate relations;
> includes new and updated code metrics, notably a new version of the
> coupling metric; allows calling a user-defined goal per test set when
> automating tests; allows automatically running tests when using the
> make tool; includes new and improved tests for Prolog standards
> compliance and Logtalk tools and libraries; provides portability
> updates for CxProlog, ECLiPSe, GNU Prolog, JIProlog, Lean Prolog,
> Quintus Prolog, SICStus Prolog, and XSB; plus other improvements and
> fixes to the documentation, compiler, library, tools, examples, and
> installers. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 4

> Logtalk 3.14.0 is now available for [downloading](download.html).
> Sponsored by Kyndi Inc., this release introduces *parameter variables*
> for simplifying handling and improving maintainability of parametric
> entities, adds new error throwing methods for simplifying error
> handling, features a new version of the code metrics that supports
> computing single metrics, includes a new version of the unit testing
> tool that supports running a set of test suites as a unified suite
> while generating a single code coverage report, adds make support for
> documentation tasks, adds an *expected terms* library and improves the
> *optional terms* library support, includes new unit tests and new and
> updated examples, plus other fixes and improvements to the compiler,
> runtime, library, and tools. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2017

#### November 17

> Two recent cool adds-ons for Logtalk:
>
> -   [webtalk - Boilerplate code for web applications written using
>     Logtalk and SWI-Prolog](https://github.com/sandogeorge/webtalk)
> -   [lgtinit - Initializes project scaffolding for Logtalk
>     projects](https://github.com/eazar001/lgtinit)

#### November 8

> Logtalk 3.13.0 is now available for [downloading](download.html).
> Sponsored by Kyndi Inc., this release features a new compiler linter
> check for trivial fails, a new code metric for documentation quality,
> alternative library paths files for simplifying application
> deployment, improved optionals library support, tool fixes and
> improvements, new unit tests, Docker fixes, and new and updated
> examples. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 10

> Logtalk 3.12.0 is now available for [downloading](download.html).
> Sponsored by Kyndi Inc., this release introduces default meta-messages
> for use with the message printing mechanism, includes new library
> predicates, improves unit testing support, adds new unit tests, and
> fixes library portability issues for CxProlog, ECLiPSe, GNU Prolog,
> JIProlog, Qu-Prolog, XSB, and YAP. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August 28

> Logtalk 3.11.2 is now available for [downloading](download.html).
> Sponsored by Kyndi Inc., this release includes runtime multi-threading
> improvements and fixes for detecting unexpected compilation failures
> caused by backend Prolog compiler issues. It also includes new library
> predicates, new tests, improved library and tools documentation,
> improved support for test and documentation automation, and
> portability updates for ECLiPSe and SWI-Prolog. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 11

> Logtalk 3.11.1 is now available for [downloading](download.html).
> Sponsored by Kyndi Inc., this release includes improvements and fixes
> for using reflection and database predicates with module-qualified
> arguments, fixes for the make and diagrams tools, and improved support
> for the the Visual Studio Code text editor. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 3

> Logtalk 3.11.0 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc. It improves support for CI servers,
> simplifies writing of type-checking code and debugging messages,
> updates the reflection API to allow enumerating included files,
> updates the make tool to be aware of included files, updates the
> diagrams tool to display included files in file diagrams, includes
> improvements and fixes for loading Logtalk into a module, plus
> documentation, library, examples, tests, and text editor support
> updates. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 14

> Logtalk 3.10.9 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc and features compiler, reflection
> API, library, and testing improvements. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 30

> Logtalk 3.10.8 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc. It fixes a compiler bug and
> includes a new optionals library, documentation improvements and
> fixes, and new unit tests. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 10

> Logtalk 3.10.7 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc and adds compiler lint checks for
> tautology and falsehood entity goals, adds support for extending the
> make tool with user-defined actions, and includes some library and
> tool bug fixes. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 1

> Logtalk 3.10.6 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc and adds a Redis client library, new
> make targets, usability improvements, and some compiler bug fixes. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April 17

> Logtalk 3.10.5 is now available for [downloading](download.html). This
> release fixes two compiler bugs and includes improvements and fixes
> for testing support. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April 6

> Logtalk 3.10.4 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc and adds support for generating code
> coverage reports in XML/HTML format for use in continuous integration
> servers. Also included are compiler, documentation, library, scripts,
> tests, examples, and coding support improvements and fixes. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 20

> Logtalk 3.10.3 is now available for [downloading](download.html). This
> release fixes a regression in the previous stable release in the
> compilation of multifile predicate clauses that make calls to the
> `::/1-2` control constructs and also fixes a spurious choice-point
> when using the `type` library object for type-checking that resulted
> in unwanted non-determinism. Also included are some compiler, library,
> and tools improvements. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 17

> A public [chat room](https://gitter.im/LogtalkDotOrg/logtalk3) for
> general discussion on Logtalk is now available.

#### March 13

> Logtalk 3.10.2 is now available for [downloading](download.html). This
> release generalizes support for multifile predicates allowing them to
> be declared protected or private, fixes some minor issues when
> printing compiler errors and warnings, adds support for
> operating-system types and stream types, adds a new programming
> example and improves some of the existing examples, includes new unit
> tests, and improves usability of the `code_metrics`,
> `dead_code_scanner`, and `make` tools. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 2

> Logtalk 3.10.1 is now available for [downloading](download.html). This
> is mainly a bug fix release. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February 27

> Logtalk 3.10.0 is now available for [downloading](download.html). This
> release is sponsored by Kyndi Inc and includes several noteworthy
> changes. It completes support for `include/1` directives, notably when
> reporting compiler errors and warnings. It changes debug events to
> account for predicates defined in included files. The compiler no
> longer changes the backend Prolog working directory when compiling
> files to avoid potential issues in multi-threaded applications. Also
> included are library, tools, and scripts fixes and improvements; new
> unit tests; improved support for the Atom text editor; and portability
> updates for CxProlog, Qu-Prolog, SICStus Prolog, SWI-Prolog, XSB, and
> YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February 15

> Logtalk 3.09.2 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. and includes a plain Prolog
> version of the Unicode standard; compiler, library, tools, and scripts
> fixes and improvements; and a first version of a IntelliJ IDEA plug-in
> contributed by Sergio Castro; new unit tests; and portability fixes
> for ECLiPSe. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 16

> Logtalk 3.09.1 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. and includes reflection API and
> compiler lint checker improvements, a code metrics developer tool
> contributed by Ebrahim Azarisooreh, Docker support contributed by
> Sergio Castro, Java interface improvements, developer tool fixes,
> extended unit tests, and portability fixes for SWI-Prolog and XSB. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2016

#### November 28

> Logtalk 3.09.0 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. and includes several additions,
> improvements, and fixes to the compiler, runtime, adapters, library,
> documentation, and developer tools. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 17

> Logtalk 3.08.0 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. and includes numerous improvements
> and fixes to the compiler, runtime, adapters, library, documentation,
> and developer tools. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August 31

> Logtalk 3.07.0 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. and includes numerous improvements
> and fixes to the compiler, runtime, adapters, library, documentation,
> and developer tools. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 18

> Logtalk 3.06.2 is now available for [downloading](download.html). This
> release is sponsored by Kyndi, Inc. It provides compiler/runtime,
> tool, and documentation improvements; unit test updates; and a
> compatibility fix for XSB-MT. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 19

> Logtalk 3.06.1 is now available for [downloading](download.html). This
> release provides the final threaded engines API. It renames some of
> the engine predicates for facilitating porting code between
> coroutining and threaded engine APIs and adds a new predicate for
> retrieving engine answers in reified form. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 12

> Logtalk 3.06.0 is now available for [downloading](download.html). This
> release highlight is a new *threaded engines* API, sponsored by Kyndi,
> Inc. Also included are updates, improvements, and fixes for the
> compiler, adapter files, tools, examples, tests, and text editor
> support. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 16

> Logtalk 3.05.0 is now available for [downloading](download.html). This
> release focus once again on improved developer tools and is sponsored
> by Kyndi, Inc. Also included are improvements and fixes for the
> compiler, adapter files, library, and tests. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 3

> Logtalk 3.04.4 is now available for [downloading](download.html). This
> release continues the work on improving the developer tools under the
> sponsorship of Kyndi, Inc. It includes a new version of the *wrapper*
> tool for porting plain Prolog applications and improvements and fixes
> for the *lgtunit* and *diagrams* tools. It also includes new unit
> tests, compiler and documentation fixes, and a compatibility update
> for Lean Prolog. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 16

> Logtalk 3.04.1 is now available for [downloading](download.html). This
> release continues the work on improved documenting and testing tools
> under the sponsorship of Kyndi, Inc. It improves and fixes issues in
> the TAP and xUnit test results output, adds output format and timeout
> options to the testing automation script, adds support for a
> `see_also` key to the `info/1` entity documenting directive, and
> improves sorting of keys in the directory, entity, and predicate
> indexes. It also includes compiler fixes and a compatibility update
> for CxProlog. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 7

> Logtalk 3.04.0 is now available for [downloading](download.html). This
> release focus on improved developer tools and is sponsored by Kyndi,
> Inc. It features improved documenting, diagraming, and testing tools.
> It also includes improvements and fixes for the compiler, adapter
> files, library, examples, and tests. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February 16

> Logtalk 3.03.0 is now available for [downloading](download.html). This
> release adds new make targets for listing missing entities, missing
> predicates, and circular references, fixes file name collisions when
> embedding an application using source files with the same name in
> different directories, fixes a bug in the optimization of
> meta-predicate calls, fixes typos in the user and reference manuals,
> and includes compatibility updates for CxProlog, GNU Prolog,
> Qu-Prolog, SICStus Prolog, SWI-Prolog, and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2015

#### December 22

> Logtalk 3.02.2 is now available for [downloading](download.html). This
> release adds library meta-predicates and hook pipeline objects,
> includes improvements to the \"help\" tool, fixes an error checking
> bug in lambda expressions, and includes a compatibility updates for
> B-Prolog. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November 12

> Logtalk 3.02.1 is now available for [downloading](download.html). This
> release adds support for incremental embedding of Logtalk
> applications, improves functionality of the make predicates, fixes
> bugs in the compilation of disjunctions when the user defines
> goal-expansion rules that add or remove conditional goals, fixes bugs
> in the support for the pseudo-object `user`, adds a user manual
> section on the optimization of applications, adds new and improves
> existing unit tests, and includes compatibility updates for Lean
> Prolog. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November 2

> Logtalk 3.02.0 is now available for [downloading](download.html). This
> release changes semantics of multifile predicates when calling
> database, reflection, and term-expansion methods; improves and fixes
> bugs in the term-expansion mechanism; fixes a static binding bug with
> some backend Prolog compilers; fixes loading of files with camel case
> names with some backend Prolog compilers; adds some more unit tests;
> and includes compatibility updates for ECLiPSe, GNU Prolog, JIProlog,
> Lean Prolog, Quintus Prolog, and XSB. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 18

> Logtalk 3.01.2 is now available for [downloading](download.html). This
> release improves documentation, developer tools, and examples; fixes
> some compiler bugs; adds a new predicate to the portable
> operating-system library; and adds a new programming example. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 30

> Logtalk 3.01.1 is now available for [downloading](download.html). This
> release improves support for complementing categories (hot patching),
> fixes a couple of compiler bugs, adds a new predicate to the portable
> operating-system library, introduces an experimental tool for helping
> porting plain Prolog code, adds a retry option to the debugger, and
> adds a new programming example. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 12

> Logtalk 3.01.0 is now available for [downloading](download.html).
> Logtalk is now distributed under the Apache License 2.0. This license
> change is kindly sponsored by [Kyndi Inc.](http://kyndi.com/)

#### September 4

> Logtalk 3.00.7 is now available for [downloading](download.html). This
> release implements a `begin_of_file` term generated when compiling a
> source file that can be used by the term-expansion mechanism, improves
> the question asking mechanism, improves error checking when using
> included files, adds missing library files accidentally omitted in the
> previous stable release, fixes minor tool bugs, adds more Prolog
> conformance unit tests, adds two examples (about using the new
> `begin_of_file` term to automatically wrap plain Prolog code in a
> source file in an object and about supporting application localization
> in multiple natural languages), adds support for the Rouge syntax
> highlighter, and includes compatibility updates for Lean Prolog and
> SICStus Prolog.

#### August 3

> Logtalk 3.00.6 is now available for [downloading](download.html). This
> release fixes bugs in the reflection API and in the processing of
> conditional compilation directives, improves library support for
> assignment variables, adds some more unit tests, and includes
> compatibility updates for GNU Prolog and Lean Prolog.

#### July 27

> Logtalk 3.00.5 is now available for [downloading](download.html). This
> release features improved documentation and improved hot patching
> support plus compatibility updates for B-Prolog, ECLiPSe, JIProlog,
> and Lean Prolog.

#### June 23

> Logtalk 3.00.4 is now available for [downloading](download.html). This
> release fixes a severe regression in the previous release in the
> compilation of source file level `multifile/1`, `discontiguous/1`, and
> `dynamic/1` directives.

#### June 22

> Logtalk 3.00.3 is now available for [downloading](download.html). This
> release features compiler improvements and fixes, an improved unit
> test framework, fixes for the Prolog conformance test suite, and
> includes compatibility updates for for JIProlog. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 27

> Logtalk 3.00.2 is now available for [downloading](download.html). This
> release features a new built-in predicate for creating flags, an
> improved unit test framework, an expanded Prolog conformance test
> suite, and includes compatibility updates for for CxProlog, JIProlog,
> Lean Prolog, Qu-Prolog, SICStus Prolog, and XSB. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February 25

> Logtalk 3.00.1 is now available for [downloading](download.html). This
> release features support for JIProlog; improvements to the reflection
> API; compiler and runtime fixes; startup, compiler, and runtime
> performance improvements; documentation updates; extended examples and
> test suites; support for creating a \"logtalk\" SWI-Prolog pack;
> usability fixes for the Mac OS X installer; and includes compatibility
> updates for for CxProlog, Qu-Prolog, Quintus Prolog, SICStus Prolog,
> SWI-Prolog, and YAP. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 7

> Logtalk 3.00.0 Stable is now available for
> [downloading](download.html). This release improves the diagrams tool,
> updates documentation, fixes a bug in the reflection API, and includes
> compatibility updates for SWI-Prolog and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2014

#### December 19

> Logtalk 3.00.0 Release Candidate 9 is now available for
> [downloading](download.html). This release improves compiler
> performance (when collecting source data), improves documentation on
> entity and predicate properties, fixes bugs in the reflection API, and
> includes compatibility updates for SWI-Prolog. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).
>
> This is a near final release of the third generation of Logtalk.
> Interested parties are invited to test their applications, specially
> if migrating from Logtalk 2.x, and report any issue as soon as
> possible.

#### December 9

> Logtalk 3.00.0 Release Candidate 8 is now available for
> [downloading](download.html). This release enforces stricter syntax
> for directives, includes compiler improvements and bug fixes, library
> compatibility fixes, tool fixes, new unit tests, and includes
> compatibility updates for B-Prolog, CxProlog, ECLiPSe, Lean Prolog,
> Quintus Prolog, Qu-Prolog, and SWI-Prolog. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### December 1

> Logtalk 3.00.0 Release Candidate 7 is now available for
> [downloading](download.html). This release includes compiler
> improvements and bug fixes, improves the Windows installer, fixes
> issues in the unit test framework, fixes issues in the Prolog
> conformance unit tests with some backend compilers, and includes
> compatibility updates for CxProlog, ECLiPSe, SICStus Prolog, and XSB.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November 19

> Logtalk 3.00.0 Release Candidate 6 is now available for
> [downloading](download.html). This release includes improvements and
> bug fixes for the compiler and runtime, updates the documentation of
> the unit test framework, adds new Logtalk unit tests and improves the
> existing Prolog conformance unit tests. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November 12

> Logtalk 3.00.0 Release Candidate 5 is now available for
> [downloading](download.html). This release includes an updated unit
> testing framework with support for testing input/output predicates,
> includes an updated documenting tool with support for exporting
> Markdown text files, improves and fixes bugs in the diagrams tool,
> fixes some compiler bugs, adds missing Prolog conformance unit tests
> for input/output predicates and improves existing unit tests, adds a
> new flag, and includes compatibility updates for ECLiPSe, JIProlog,
> Lean Prolog, SICStus Prolog, and YAP. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 28

> Logtalk 3.00.0 Release Candidate 4 is now available for
> [downloading](download.html). This release completes the static
> binding implementation; adds support for using file names as-is with
> the compiling and loading predicates; fixes compiler bugs; features
> documentation updates; improves the debugging, testing, and
> documenting tools; adds a new set of unit tests for checking Prolog
> conformance with official and de facto standards; updates syntax
> coloring for all supported text editors and syntax highlighters; and
> includes compatibility updates for ECLiPSe, JIProlog, and YAP. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 3

> Logtalk 3.00.0 Release Candidate 3 is now available for
> [downloading](download.html). This release restricts
> `initialization/1` directives to source files and objects, changes
> some of the debugging events, adds preliminary support for Jekejeke
> Prolog and JIProlog, fixes issues with some Prolog adapter files,
> fixes issues with the debugger and unit testing tools, adds a new
> programming example, and includes documentation updates. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 22

> Logtalk 3.00.0 Release Candidate 2 is now available for
> [downloading](download.html). This release adds support for compiling
> Prolog source files as Logtalk code without requiring changing the
> file name extension, supports the definition of multiple Prolog file
> name extensions, reverts the restriction of primary multifile
> predicate declarations to objects, improves and fixes bugs in the
> documenting and unit testing tools, includes documentation updates,
> improves Pygments and SubEthaEdit syntax coloring support, and adds a
> completions file for Sublime Text. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 3

> Logtalk 3.00.0 Release Candidate 1 is now available for
> [downloading](download.html). This release fixes long standing
> meta-predicate execution context issues inherited from Logtalk 2.x,
> improves meta-predicate semantics by ensuring that meta-arguments are
> always called with the caller full execution context, refines and
> improves multifile predicate semantics, adds a new token to the
> structured message printing mechanism, features a new [port profiler
> tool](http://forums.logtalk.org/viewtopic.php?f=21&t=240), improves
> the debugger and diagrams tools, fixes all known bugs, includes
> documentation and unit test updates, and SWI-Prolog, XSB, and YAP
> compatibility improvements. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 31

> Logtalk 3.00.0 Beta 9 is now available for
> [downloading](download.html). This release includes top-level
> interpreter usability improvements, compiler optimizations for
> meta-calls, documentation updates, improved developer tools (in
> particular, the debugger tool now supports line number spy points and
> the diagrams tool can now generate diagrams for Prolog module
> applications when using SWI-Prolog or YAP as backend compilers), and
> Lean Prolog and SICStus Prolog compatibility fixes. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 4

> Logtalk 3.00.0 Beta 8 is now available for
> [downloading](download.html). This release includes a new structured
> question asking mechanism complementing the structured message
> printing mechanism already in place, introduces less restrictive
> licensing terms, improves the debugger and diagrams tools, adds a new
> programming example, and fixes some bugs. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 11

> Logtalk 3.00.0 Beta 6 is now available for
> [downloading](download.html), featuring a simpler, smaller, and faster
> compiler. The full
> [announcement](http://forums.logtalk.org/viewtopic.php?f=21&t=234) is
> posted on the Logtalk discussion forums.

#### April 9

> Logtalk 3.00.0 Beta 1 is now available for
> [downloading](download.html). The full
> [announcement](http://forums.logtalk.org/viewtopic.php?f=21&t=228) is
> posted on the Logtalk discussion forums.

#### January 15

> A new, much improved, diagrams tool is included with the [Logtalk
> 3.00.0 Alpha 33 release](download.html). See the separate
> [announcement](http://forums.logtalk.org/viewtopic.php?f=21&t=222) for
> the highlights.

### 2013

#### November 1

> Installers for the latest Logtalk 3 development version are now
> [available](download.html) on a regular basis.

#### April 10

> New development versions of Logtalk 3 are regularly released and
> available from our
> [GitHub](https://github.com/LogtalkDotOrg/logtalk3/) account. Despite
> the current *alpha* tag, this releases are fully tested and
> recommended over the latest Logtalk 2 stable version.

#### February 11

> Logtalk 3.00.0 Alpha 9 is now
> [available](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 18

> Logtalk 3.00.0 Alpha 8 is now
> [available](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2012

#### December 16

> The old Logtalk Trac website was broken by recent \"upgrades\" by my
> host provider. Some of the information there have been salvaged and
> moved to the [GitHub](https://github.com/LogtalkDotOrg/logtalk3/wiki)
> repository, which is now the official place for Logtalk development.

#### October 12

> Logtalk 3.00.0 Alpha 3 is now available at
> [GitHub](https://github.com/LogtalkDotOrg).
>
> A new Windows installer for Logtalk 2.44.1 is now
> [available](download.html). It supports detection of the new SICStus
> Prolog 4.2.3 64 bits Windows version (previous Windows versions are 32
> bits only).

#### September 20

> A new Windows installer for Logtalk 2.44.1 is now
> [available](download.html). It solves an issue where SWI-Prolog 6.3.1
> (and later versions) would not be detected on 64 bits systems due to
> changes in the used registry keys.

#### August 21

> Logtalk 3.00.0 Alpha 1 is now available at
> [GitHub](https://github.com/LogtalkDotOrg).

#### August 17

> Logtalk 3.x development is now hosted at
> [GitHub](https://github.com/LogtalkDotOrg). The
> [license](https://github.com/LogtalkDotOrg/logtalk3/blob/master/LICENSE.txt)
> for this release is now live for earlier
> [feedback](http://forums.logtalk.org/viewtopic.php?f=21&t=182). The
> [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
> for the current (private) development version are also available.
>
> Logtalk 2.x development is frozen now that Logtalk 3.x is in full
> development. No more updates to Logtalk 2.x are expected.

#### May 28

> Logtalk 2.44.1 is now available for [downloading](download.html). This
> release updates the semantics of \"before\" event handlers, provides
> more consistent handling of compiler options, corrects a bug in the
> compilation of the `meta_non_terminal/1` directive, improves the unit
> test framework, fixes several bugs in the Windows installer, includes
> portability updates for ECLiPSe, XSB, and YAP plus updates to the
> library, examples, and text editor support. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 7

> Logtalk 2.44.0 is now available for [downloading](download.html). This
> release changes the semantics of complementing categories, allowing
> its use to patch existing object code, fixes two bugs in the
> processing of meta-calls, allows open lists of terminals in the body
> of DCG rules, adds two new examples, and improves support for the Vim
> text editor and for Exuberant ctags. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2011

#### December 21

> Logtalk 2.43.3 is now available for [downloading](download.html). This
> release extends the `uses/2` directive semantics, adds a `scope/1`
> predicate property, features compiler and runtime improvements that
> simplify building applications where Logtalk libraries are
> pre-compiled and pre-loaded, adds new list library predicates, and
> includes portability updates for Lean Prolog and SWI-Prolog. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 4

> Logtalk 2.43.2 is now available for [downloading](download.html). This
> is a minor release with some bug fixes and minor compiler and runtime
> improvements. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 12

> Logtalk 2.43.1 is now available for [downloading](download.html). This
> release includes a parser for PDDL 3.0 files contributed by Robert
> Sasak, improved coinduction support, new compiler flags allowing
> passing options to the back-end Prolog compiler, improved
> meta-predicate support, updated examples, minor dynamic binding
> performance improvements, updated support for several text editors,
> fixes for all know bugs, and portability updates for ECLiPSe, Lean
> Prolog, Qu-Prolog, SICStus Prolog, XSB, and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July 31

> Logtalk 2.43.0 is now available for [downloading](download.html). This
> is a major release. Highlights include revamped support for structural
> reflection, improved coinduction support, major internal and
> user-level changes to exception handling and reporting, portability
> updates, fixes for all know bugs, and a new Windows installer that can
> be used by non-admin users. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April 4

> Logtalk 2.42.4 is now available for [downloading](download.html). This
> release includes compiler, runtime, and multi-threading performance
> optimizations, improves compiler error messages for the
> `synchronized/1` and `dynamic/1` directives, adds support for
> preserving operator scope information and outputting this information
> to the automatically generated XML documenting files, adds new utility
> predicates to the `logtalk` object, improves several programming
> examples, includes a workaround for a SWI-Prolog uninstaller bug on
> Windows, and features portability updates for Qu-Prolog, SICStus
> Prolog, SWI-Prolog, XSB, and YAP. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 20

> Updated the Logtalk [performance](performance.html) web page with
> benchmark test results for all supported back-end Prolog compilers.

#### February 21

> Logtalk 2.42.3 is now available for [downloading](download.html). This
> release adds support for calling dynamic predicates in the context of
> *this* from within categories, adds support for pre-compiled clause
> heads, includes bug fixes and improvements to the built-in debugger,
> includes improved libraries and examples, adds support for indexicals
> when using the SICStus Prolog CLP(FD) library, adds an experimental
> example of using attributed variables within objects and categories,
> and features portability updates for ECLiPSe, GNU Prolog, SICStus
> Prolog, and SWI-Prolog. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 25

> Logtalk 2.42.2 is now available for [downloading](download.html). This
> release improves the compilation of calls to module predicates;
> improves checking of meta-arguments in meta-predicate calls; improves
> support for lambda expressions; includes an optimizing compiler for
> calls to library meta-predicates; adds new libraries for logging
> events, working with temporal interval relations, and using integer
> counters; improves existing examples and libraries; adds support for
> using the JavaScript-based SyntaxHighlighter package; and features
> portability updates for GNU Prolog, Qu-Prolog, SICStus Prolog,
> SWI-Prolog, and XSB. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2010

#### December 22

> Logtalk 2.42.1 is now available for [downloading](download.html). This
> release adds support for new meta-predicate mode indicators, enabling
> support for more Prolog proprietary built-in meta-predicates; adds
> support for detecting and reporting missing `dynamic/1` and
> `discontiguous/1` directives; adds a new lint flag; corrects two
> meta-predicate compilation bugs; updates some of the examples, and
> includes portability updates for B-Prolog, SICStus Prolog, SWI-Prolog,
> XSB, and YAP. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### December 1

> Logtalk 2.42.0 is now available for [downloading](download.html). This
> release adds support for the SICStus Prolog, SWI-Prolog, and YAP
> profilers; adds preliminary support for generating entity diagrams for
> source files and libraries; improves the experimental support for
> ProbLog; adds experimental support for CHR; adds support for B-Prolog
> Action Rules; defines a set of low-level utility predicates available
> from the \"logtalk\" built-in object; improves the performance of
> source file compilation, dynamic binding, and database built-in
> methods; enhances the term-expansion mechanism; fixes all know bugs;
> adds new examples and features minor updates to existing examples and
> to the library; and includes portability updates for B-Prolog, GNU
> Prolog, Qu-Prolog, SWI-Prolog, XSB, and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October 6

> Logtalk 2.41.1 is now available for [downloading](download.html). This
> release simplifies the definition of class hierarchies when reflexive
> designs are not required, simplifies the internal representation of
> compiled entities, adds support for the blackboard built-in predicates
> when running on a back-end Prolog compiler supporting this feature,
> fixes all know bugs, features minor updates to some examples and the
> standard library, and includes portability updates for SICStus Prolog,
> SWI-Prolog, and YAP. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 15

> Logtalk 2.41.0 is now available for [downloading](download.html). This
> release adds support for coinductive predicates, adds a new built-in
> predicate for accessing the Logtalk compilation/loading context, adds
> new programming examples, adds support for the SHJS syntax
> highlighter, fixes all know bugs, and includes portability updates for
> CxProlog, ECLiPSe, SWI-Prolog, XSB, and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 30

> Logtalk 2.40.1 is now available for [downloading](download.html). This
> release restores support for GNU Prolog (requires version 1.4.0),
> updates syntax coloring and code completion support for supported text
> editors and syntax highlighters, improves several examples and adds
> more example unit tests, improves the unit tests automation script,
> fixes all know bugs, and includes portability updates for B-Prolog,
> Ciao, CxProlog, SWI-Prolog, and YAP. For details and a complete list
> of changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 23

> Added a list of Logtalk contributors and a list of open-source
> projects used in Logtalk to the [documentation](documentation.html)
> web page.

#### June 16

> Logtalk 2.40.0 is now available for [downloading](download.html). This
> release implements a `call//1` built-in non-terminal, changes the
> scope of the built-in methods `phrase/2-3` for more consistent
> meta-predicate semantics, clarifies the scope of the term-expansion
> and goal-expansion mechanisms, fixes all known bugs, adds experimental
> on-line help support, adds man pages for all POSIX shell scripts,
> bundles Victor Lagerkvist\'s Verdi Neruda (a meta-interpreter
> collection that includes both top-down and bottom-up search
> strategies), and includes portability updates for Ciao Prolog,
> ECLiPSe, Qu-Prolog, SWI-Prolog, XSB, and YAP. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 2

> An experimental Logtalk git repository is now available from
> [github](http://github.com/pmoura/logtalk). This git repository tracks
> the trunk of the [Logtalk Subversion
> repository](http://svn.logtalk.org/). The goal is to make it easier
> for users to fork Logtalk, either to customize it for internal use or
> for contributing back to Logtalk. Be sure to check and comply with the
> Logtalk [license](license.html) if you plan to distribute your
> modified versions.

#### May 4

> Logtalk 2.39.2 is now available for [downloading](download.html). This
> release optimizes the internal representation of entity and predicate
> properties, improves reflection support, improves unit testing
> support, improves interoperability with Prolog module libraries, fixes
> all known bugs, and includes portability updates for B-Prolog,
> ECLiPSe, Qu-Prolog, SICStus Prolog, SWI-Prolog, XSB, and YAP. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March 31

> Logtalk 2.39.1 is now available for [downloading](download.html). This
> release includes a new and improved support for unit testing, adds a
> set of unit tests based on the examples sample queries, improves
> multi-threading support, adds runtime safety to the `uses/2`
> directive, improves libraries and programming examples, fixes all
> known bugs, improves the Windows installer, and includes portability
> updates for Ciao, CxProlog, ECLiPSe, XSB, and YAP. A special thanks to
> Parker Jones for his contributions to this release. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February 28

> Logtalk 2.39.0 is now available for [downloading](download.html). This
> release removes support for outdated Prolog compilers and for Prolog
> compilers that don\'t support the standard directive `multifile/1` or,
> in general, that do not provide support for de facto and official
> standards. In addition, this release reintroduces parametric
> categories and changes semantics of the `parameter/2` built-in
> execution-context method when used in category predicates, removes an
> overly restrictive meta-predicate compilation rule, adds
> meta-predicates `sort/3` and `msort/3` to the library object `list`,
> adds library implementations of red-black trees and heaps, improves
> the benchmarking test suits, improves several examples, and updates
> the Windows installer in order to detect Prolog compilers
> installations on 64 bits version of Windows. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January 31

> Logtalk 2.38.2 is now available for [downloading](download.html). This
> release improves suport for the `:/1` control construct, simplifies
> parsing of proprietary directives in config files, corrects a compiler
> bug where redefinitions of Prolog built-in predicates would be
> ignored, and includes compatibility updates for B-Prolog, ECLiPSe,
> SICStus Prolog, SWI-Prolog, XSB, and YAP. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2009

#### December 21

> Logtalk 2.38.1 is now available for [downloading](download.html). This
> release features improved support for module meta-predicates,
> meta-calls, and lambda expressions; improved compiler error-checking
> for meta-predicate directives; bug fixes; updated syntax coloring
> support; and includes compatibility updates for B-Prolog, CxProlog,
> SWI-Prolog, XSB, and YAP. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### December 3

> Logtalk 2.38.0 is now available for [downloading](download.html). This
> release features support for lambda expressions, support for using the
> `set_logtalk_flag/2` directive within entities, improved `<</2`
> control construct, improved unit testing support, some bug fixes,
> small performance improvements, fixes syntax coloring issues with
> Pygments and SubEthaEdit, and includes compatibility updates for
> ECLiPSe, GNU Prolog, SICStus Prolog, SWI-Prolog, XSB, and YAP. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November 12

> A bug was found on the Logtalk 2.37.5 Debian and MacOS X installers
> that may result in loss of some third-party mime-type associations. In
> the case of the MacOS X installer the problem can only affect MacPorts
> users. Updated installers are now available from the
> [download](download.html) page.

#### October 29

> Logtalk 2.37.5 is now available for [downloading](download.html). This
> release features improved multi-threading support, several bug fixes,
> small performance improvements, snippets and tools support for the
> Gedit text editor, revamped GeSHi support, and includes installer
> support for adding the Logtalk mime-type to Linux and Windows systems.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September 18

> Logtalk 2.37.4 is now available for [downloading](download.html). This
> release features minor bug fixes, small performance and usability
> improvements, plus compatibility updates for B-Prolog, ECLiPSe,
> Qu-Prolog, and SICStus Prolog. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August 19

> You can now follow Logtalk development on
> [Twitter](http://twitter.com/LogtalkDotOrg).

#### August 10

> Logtalk 2.37.3 is now available for [downloading](download.html). This
> release provides portability and usability enhancements, corrects an
> optimization bug, includes library updates, improves text editor
> support, fixes typos in the documentation, and includes compatibility
> updates for ECLiPSe, GNU Prolog, and SWI-Prolog. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 29

> Logtalk 2.37.2 is now available for [downloading](download.html). This
> release optimizes performance of meta-predicates when using static
> binding, improves compilation of Prolog modules as Logtalk objects,
> improves Prolog migration support for multifile predicates, expands
> support for using grammar rule non-terminal indicators in predicate
> directives, fixes know bugs, and includes compatibility updates for
> B-Prolog, ECLiPSe, GNU Prolog, SICStus Prolog, SWI-Prolog, XSB, and
> YAP. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June 2

> Logtalk 2.37.1 is now available for [downloading](download.html). This
> release improves Prolog migration support for multifile predicates,
> improves integration with the CLP(FD) constraint library, improves
> automatic documentation support, features extended Logtalk libraries,
> includes new programming examples, fixes know bugs, improves Vim
> support, and includes compatibility updates for B-Prolog, ECLiPSe, GNU
> Prolog, SWI-Prolog, XSB, and YAP. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May 11

> Logtalk 2.37.0 is now available for [downloading](download.html). This
> release focus on improving Logtalk performance, specially when using
> dynamic binding, in improving meta-predicate support and semantics.
> Also included are extended Logtalk libraries and compatibility updates
> for Ciao, ECLiPSe, and Qu-Prolog. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April, 9

> Logtalk 2.36.0 is now available for [downloading](download.html). This
> release improves Logtalk customization by adding support for settings
> files, forgoing the need to directly edit the back-end Prolog compiler
> configuration flags; improves compiler error and warning reporting;
> improves SWI-Prolog integration scripts; fixes compatibility issues
> with Amzi! Prolog, Ciao Prolog, K-Prolog, Qu-Prolog, and SICStus
> Prolog; adds new object and category properties; adds new compiler
> flags; fixes a bug in the compilation of Prolog modules as objects
> introduced in the previous release; improves installation and
> integration scripts; and improves XML documentation for objects,
> categories, and predicates. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March, 1

> Logtalk 2.35.1 is now available for [downloading](download.html). This
> release improves support for using module meta-predicates and explicit
> module qualified calls in object and category predicates, improves
> support for object proxies, improves compilation reports, corrects a
> bug in the implementation of the `smart_compilation` compiler flag,
> improves support for ECLiPSE and GNU Prolog, improves the installers
> documentation, and includes updated config files for all Prolog
> compilers. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 9

> The Logtalk blog moved to a new home. It\'s now available at
> <http://blog.logtalk.org/>. Please update your bookmarks.

#### January, 16

> Logtalk 2.35.0 is now available for [downloading](download.html). This
> release improves compilation of source code, resulting in better
> performance for most back-end Prolog compilers and in more compact
> intermediate Prolog code, improves caching of message sending
> predicate lookups and \"super\" calls, simplifies compilation adds
> support for the specialization of meta-predicates, corrects a few
> bugs, and includes updated config files for SWI-Prolog, YAP, and Ciao.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 11

> Updated the [benchmarks](performance.html) page with results for the
> forthcoming Logtalk 2.35.0 release.

### 2008

#### December, 8

> Logtalk 2.34.1 is now available for [downloading](download.html). This
> release allows the `^^/1` control construct (\"super\") to call any
> inherited predicate, fixes a bug on the implementation of the `<</2`
> control construct when used at the top-level, improves error checking
> when compiling source files, fixes some broken links in the Logtalk
> XHTML documentation, adds a set of double-clickable `*.command`
> Terminal.app files for starting Logtalk with selected back-end Prolog
> compilers on MacOS X, and improves the MacOS X installer. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 26

> Logtalk 2.34.0 is now available for [downloading](download.html). This
> release adds support for conditional compilation in source files,
> improves term and goal expansion mechanisms, adds a new compiler flag
> for identifying back-end Prolog compilers, corrects some minor bugs,
> and includes new and improved programming examples. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 3

> Logtalk 2.33.2 is now available for [downloading](download.html). This
> release enhances complementing category support, improves the Logtalk
> compiler error reporting, adds optimization and safety compiler
> options, adds entity source file properties, improves the built-in
> debugger, and includes new and improved programming examples. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 12

> Logtalk 2.33.1 is now available for [downloading](download.html). This
> release adds a syntax construct for easy access to parametric object
> proxies, improves the built-in debugger, enhances the entity creation
> built-in predicates and the built-in database methods, adds new
> libraries and new examples, improves existing libraries and examples,
> and updates support for the CxProlog, ECLiPSe, K-Prolog, and XSB
> compilers. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 1

> Logtalk 2.33.0 is now available for [downloading](download.html). This
> release improves support for using Prolog module libraries, provides
> several examples of using constraints within objects, optimizes
> multi-threading performance, adds support for using the
> `ensure_loaded/1` and the `set_prolog_flag/2` directives in source
> files, corrects several bugs, and updates support for the ECLiPSe, GNU
> Prolog, and SWI-Prolog compilers. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July, 26

> Logtalk 2.32.2 is now available for [downloading](download.html). This
> release simplifies and optimizes the code generated by the compilation
> of source files, optimizes and updates the `^^/1` control construct to
> allow its use within categories, improves the readability of compiler
> messages, corrects some bugs in the database built-in methods,
> restores redefined entity warnings for Prolog back-end compilers
> supporting multifile predicates, adds new programming examples, adds
> experimental support for the GeSHi syntax highlighter, improves
> support for the Pygments syntax highlighter, and updates support for
> the SWI-Prolog, B-Prolog, YAP, SICStus, XSB, and GNU Prolog compilers.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July, 7

> Logtalk 2.32.1 is now available for [downloading](download.html). This
> release changes the representation of the runtime tables for loaded
> entities, restores redefined entity warnings for Prolog back-end
> compilers supporting multifile predicates, corrects a bug with
> predicate aliases and the `:/1` control construct, improves support
> for the Vim text editor and for the Pygments syntax highlighter, and
> updates support for the SWI-Prolog, CxProlog, K-Prolog, and B-Prolog
> compilers. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June, 16

> Logtalk 2.32.0 is now available for [downloading](download.html). This
> release updates multi-threading features and examples, improves
> support for compiling and loading source files with a large number of
> entities, updates support for Yap and Quintus Prolog, and includes
> updated support for the Vim text editor. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May, 26

> Logtalk 2.31.6 is now available for [downloading](download.html). This
> release improves support for several text editors and syntax
> highlighters, fixes some bugs when using predicate aliases and the
> `:/1` control construct with categories that extend other categories,
> and includes updated YAP and SWI-Prolog config files. For details and
> a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### April, 29

> Logtalk 2.31.5 is now available for [downloading](download.html). This
> release improves support for multi-threading programming, adds support
> for checking arithmetic expressions for calls to non-portable
> functions when using the `portability` compiler flag, updates several
> Prolog config files, includes new examples, and adds support for
> generating plain text files from XML documenting files. Other changes
> include bug fixes and improvements to library objects and text editing
> support. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 29

> The Logtalk developers [website](http://trac.logtalk.org/) is now
> on-line. The website uses [Trac](http://trac.edgewall.org/), an open
> source web-based software project management and bug/issue tracking
> system.

#### February, 20

> Logtalk 2.31.4 is now available for [downloading](download.html). This
> release updates the support for multi-threading programming,
> correcting bugs and improving performance. New and improved
> multi-threading examples are also included. Other changes include bug
> fixes and improvements to library objects and text editing support.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 28

> Logtalk 2.31.3 is now available for [downloading](download.html). This
> release updates installer and integration scripts for detecting
> outdated Logtalk user data folders, improves support for the
> `encoding/1` directive, and corrects a problem with the Quintus Prolog
> integration scripts. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 21

> Logtalk 2.31.2 is now available for [downloading](download.html). This
> release updates support for the `encoding/1` directive, adding
> compatibility with CXProlog 0.96.3 and SICStus Prolog 4.0 and
> improving support for YAP and SWI-Prolog. For details and a complete
> list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 3

> Logtalk 2.31.1 is now available for [downloading](download.html). This
> release updates some of the multi-threading examples, improves the
> support for the TextMate text editor, and updates support for YAP and
> SWI-Prolog. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2007

#### December, 21

> Logtalk 2.31.0 is now available for [downloading](download.html). This
> release implements new category functionality, revamps the support for
> compiler hooks, adds a new built-in protocol for term and goal
> expansion predicates, includes new and updated examples, and updates
> support for B-Prolog, CxProlog, K-Prolog, XSB, and YAP. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 9

> Logtalk 2.30.8 is now available for [downloading](download.html). This
> release fixes a bug in the compilation of synchronized predicates that
> breaks Logtalk on single-threaded Prolog compilers. The bug is present
> in the two previous Logtalk versions.

#### November, 5

> Logtalk 2.30.7 is now available for [downloading](download.html). This
> release improves support for multi-threading programming, fixes issues
> in some examples, adds a new compiler flag and a new multi-threading
> example, and updates the config files of B-Prolog, SICStus Prolog,
> SWI-Prolog, YAP, and XSB. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 21

> Re-release Logtalk 2.30.6 due to a bug in the compiler that slipped in
> while packaging. If you\'ve already download this version, please
> download it again. Sorry for the trouble.

#### October, 20

> Logtalk 2.30.6 is now available for [downloading](download.html). This
> release improves support for multi-threading programming and Unicode,
> renames several compiler options for clarity, adds syntax coloring
> support for GtkSourceView 2, and includes workarounds for problems
> with the Logtalk built-in debugger and compiler when using some
> back-end Prolog compilers. For details and a complete list of changes,
> please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 19

> Logtalk 2.30.5 is now available for [downloading](download.html). This
> release improves support for multi-threading programming, including
> documentation updates and new built-in predicates supporting the use
> of threaded call identifier tags in asynchronous calls. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 22

> Logtalk 2.30.4 is now available for [downloading](download.html). This
> release adds preliminary support for unit tests, includes new and
> updated examples, updates the configuration files for Qu-Prolog and
> XSB, and improves syntax coloring support for XEmacs and jEdit. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 12

> Preliminary work on Logtalk unit tests support is available from the
> URL <http://logtalk.org/files/lgtunit/logtalk_unit_tests.tar.gz>. Your
> feedback is appreciated.
>
> The Logtalk [benchmarks](performance.html) page have been updated with
> performance data on using imported category predicates.

#### July, 9

> Logtalk 2.30.3 is now available for [downloading](download.html). This
> release improves the Logtalk support for multi-threading programming.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June, 24

> Logtalk 2.30.2 is now available for [downloading](download.html). This
> release improves the Logtalk compiler error checking, fixes a bug in
> the implementation of the multi-threading built-in predicate
> `threaded_ignore/1`, and includes new and revamped examples. For
> details and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### June, 12

> Logtalk 2.30.1 is now available for [downloading](download.html). This
> release includes preliminary support for static binding when using
> imported category predicates, adds a new control construct allowing a
> goal to be proved within the context of a specified object (useful for
> debugging and for writing unit tests), and improves support for
> multi-threading programming. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May, 28

> Logtalk 2.30.0 is now available for [downloading](download.html). This
> release includes numerous improvements including preliminary support
> for static binding, simplified installation, extended Prolog
> integration, revamped support for multi-threading programming, new
> compiler options, enhanced debugging support, and some important bug
> fixes. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May, 11

> The Logtalk Subversion server is now
> [on-line](http://svn.logtalk.org/), replacing the CVS service. Its
> current contents are the result of the conversion of the current CVS
> repository using the wonderful [cvs2svn](http://cvs2svn.tigris.org/)
> tool.
>
> Installers for the Logtalk 2.30.0 beta version are now available. See
> the announcement on the [Logtalk discussion
> forums](http://forums.logtalk.org/).

#### May, 10

> Logtalk is now hosted on a commercial hosting provider. This hosting
> solution allows me to offer a set of useful services, which include a
> Subversion server, discussion forums, and a wiki. The Subversion
> server will soon replace the current CVS service. The discussion
> forums are [ready for you to use](http://forums.logtalk.org/). These
> discussion forums, together with a [new (announcements-only) mailing
> list](mlform.html), replace the older discussion mailing list, which
> is now closed. I would like to take this opportunity to thank the
> University of Coimbra, Portugal, for kindly hosting the Logtalk web
> site and mailing list for all these years.

#### March, 28

> Logtalk 2.29.5 is now available for [downloading](download.html). This
> release includes improved support for multi-threading programming,
> improved performance for dynamic predicates, improved debugging
> support, new and updated examples, and adds a new compiler option for
> specifying the action to take when reloading source files. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 19

> Logtalk 2.29.4 is now available for [downloading](download.html). This
> release provides extended support for multi-threading programming,
> improves support for some text editors, and fixes two bugs in the
> Logtalk compiler. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 15

> Logtalk 2.29.3 is now available for [downloading](download.html). This
> release fixes two important bugs in the Logtalk compiler optimizer
> code that may result in runtime errors when using the built-in
> database methods. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 10

> Logtalk 2.29.2 is now available for [downloading](download.html). This
> release improves the Logtalk experimental support for multi-threading
> programming. For details and a complete list of changes, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2006

#### December, 28

> Logtalk 2.29.1 is now available for [downloading](download.html). This
> release adds a Logtalk version of [John Fletcher\'s Prolog XML
> parser](http://www.zen37763.zen.co.uk/xml.pl.html), improves the MacOS
> X installer package, improves support for some Prolog compilers, and
> fixes a couple of bugs in the Logtalk compiler and in the library
> objects. For details and a complete list of changes, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### December, 18

> Logtalk 2.29.0 is now available for [downloading](download.html). This
> release revamps the experimental support for multi-threading
> programming and the support for event-programming, adds a new built-in
> object for more flexibility when designing class-based hierarchies,
> adds a built-in protocol declaring the event handler predicates,
> improves some of the programming examples, works around bugs in
> Internet Explorer 7 and Opera 9 rendering the XHTML manual index
> pages, and fixes some bugs in the Logtalk compiler, in the Windows
> documentation scripts, and in the Logtalk DTD file. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 6

> Logtalk 2.28.2 is now available for [downloading](download.html). This
> release includes basic support for some more MacOS X and Windows text
> editors, improves integration with SWI-Prolog, fixes a compiler bug,
> and provides support for easily creating PDF versions of the User and
> Reference Manuals (available as a separate download). For details and
> a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 10

> Logtalk 2.28.1 is now available for [downloading](download.html). This
> release includes minor feature enhancements regarding the processing
> of XML documenting files and the Linux RPM installer. It also fixes a
> typo on the \"logtalk.dtd\" file on version 2.28.0 that prevents
> validation of XML documenting files that use a local reference to the
> DTD. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 28

> Logtalk 2.28.0 is now available for [downloading](download.html). This
> release includes major features and important bug fixes. Major
> highlights are experimental support for multi-threading programming,
> much improved support for defining meta-predicates, improved
> integration with several Prolog compilers (including B-Prolog,
> ECLiPSe, SICStus Prolog, SWI-Prolog, XSB, and YAP), a new Windows GUI
> installer and an improved Linux RPM package. For details and a
> complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 15

> The second beta version of Logtalk 2.28.0 is now available in source
> form from the [CVS](cvs.html) server. Installers for [Linux (RPM
> package)](files/beta2280/logtalk-2.28.0-1.noarch.rpm) and
> [Windows](files/beta2280/lgt2280.exe) are also available. They install
> the CVS version of Logtalk 2.28.0 as of September 15. Your feedback is
> most welcome.

#### July, 18

> A [beta version of the new Logtalk Linux RPM
> package](files/beta2280/logtalk-2.28.0-1.noarch.rpm) is now available
> for testing. It installs the CVS version of Logtalk 2.28.0 as of July
> 18. This new package automatically sets the LOGTALKHOME environment
> variable to the Logtalk installation directory and defines a default
> value for the LOGTALKUSER environment variable. In addition,
> integration scripts for selected Prolog compilers are automatically
> created. Your feedback and suggestions for improvements are most
> welcome.
>
> A new [beta version of the Logtalk Windows
> installer](files/beta2280/lgt2280.exe) is also available.

#### June, 28

> A [beta version of the new Logtalk Windows
> installer](files/beta2280/lgt2280.exe) is now available for testing.
> The installer is built using Inno Setup 5 and should provide a much
> better installing experience for Windows users. The installer requires
> either Windows 2000 or Windows XP and WSH 5.6. It installs the CVS
> version of Logtalk 2.28.0 as of June 28. It may be used by
> administrative users for a full installation (including integration
> with selected Prolog compilers) and by non-administrative users for
> installing user data files on their home directories (task previously
> done by running the \"cplgtdirs\" batch script). Your feedback and
> suggestions for improvements are most welcome.

#### May, 15

> A problem was found on the Windows version of YAP which prevents the
> use of library notation for loading source files. The problem does not
> exist in versions of YAP for other operating systems. A new config
> file for YAP is now [available](files/update2271/yap.config),
> providing a workaround for the problem.

#### April, 26

> An alpha version of Logtalk 2.28.0, featuring support for
> multi-threading programming in selected Prolog compilers, is now
> available from the [CVS](cvs.html) server.

#### March, 27

> Logtalk 2.27.1 is now available for [downloading](download.html). This
> release includes optimizations to the size of the code generated when
> compiling source files, two new examples, and small improvements to
> library objects, installation scripts, and Prolog configuration files.
> For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 9

> Logtalk 2.27.0 is now available for [downloading](download.html). This
> release features improved support for grammar rules with a new grammar
> rule translator, improved performance for the `phrase/2-3` built-in
> methods, and support for declaring non-terminal aliases in `alias/3`
> directives. In addition, this release adds support for a compiler
> hook, new examples, new library objects, a new `non_terminal/1`
> predicate property, and includes a few bug fixes and improvements to
> some Prolog configuration files. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).
>
> As some of you may have noticed, today marks the 7th birthday of the
> final release of Logtalk 2.0 :-)

### 2005

#### December, 23

> Updated the [benchmark results](performance.html) web page for the
> current YAP CVS version, which contains new optimizations for PowerPC
> processors.

#### December, 20

> Logtalk 2.26.2 is now available for [downloading](download.html). This
> release features improved message sending performance, improved
> error-checking for the Logtalk compiler and for the grammar rule
> translator, improved support for XSB and Amzi! Prolog, and some bug
> fixes. For details and a complete list of changes, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 28

> Logtalk 2.26.1 is now available for [downloading](download.html). This
> release features improvements related to the Logtalk documentation, to
> the shell scripts used for converting XML documenting files into XHTML
> and PDF, and to the XSLT files used for the conversion. For details
> and a complete list of changes, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 7

> Logtalk 2.26.0 is now available for [downloading](download.html). This
> release major highlights are support for defining predicate aliases
> when using `uses/2` directives and support for compiling and using
> Prolog modules as Logtalk objects (complemented by a new Prolog
> integration and migration guide). The new support for compiling Prolog
> modules allows you to easily reuse many of the libraries that are
> distributed with common Prolog compilers. Other noteworthy changes are
> improved documentation, improvements to installation and documenting
> scripts, simplification of installation instructions, consolidation of
> most example source files into single source files, and support for
> ignoring, copying as-is, or rewriting proprietary Prolog directives
> when compiling source files. For details and a complete list of
> changes, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 12

> Logtalk 2.25.3 is now available for [downloading](download.html). This
> release improves documentation of several examples, consolidates
> source files of several examples into single source files, corrects
> some typos on the Logtalk -- B-Prolog integration instructions, and
> includes other small improvements. For details, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 11

> Logtalk 2.25.2 is now available for [downloading](download.html). This
> release corrects some bugs on the installation and Prolog integration
> shell scripts. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 8

> Logtalk 2.25.1 is now available for [downloading](download.html). This
> release adds support for the Lorenzo Bettini\'s \"source-highlight\"
> package, features improved support for several text editors, improves
> documenting scripts, includes a new state-space search example, and
> corrects a few minor bugs. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May, 23

> Logtalk 2.25.0 is now available for [downloading](download.html). This
> release features a source file-based compiler, improved compiler
> reporting, new or improved examples, and updated support for B-Prolog.
> For details, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### May, 4

> The beta version of Logtalk 2.25.0 is now available from the [CVS
> server](cvs.html), featuring a source file-based compiler, replacing
> the entity-based compiler in previous versions. The source metafile
> hack is no longer needed or supported. Logtalk source files may now
> contain any number of objects, categories, and protocols, interleaved
> with Prolog directives and clauses.

#### April, 26

> Added to the web site an usage [example](contributions/index.html) of
> the new documenting keys introduced on Logtalk 2.24.0.

#### April, 25

> A bug on the Logtalk DarwinPorts portfile as found which results on a
> wrong path to the `cplgtdirs` script for the MacOS X installer
> package. If you have download the installer package before this date,
> please download it again. Note that this is a problem with the
> installer package creation, not with Logtalk itself. Therefore, the
> remaining distribution files for Logtalk 2.24.0 are not affected.

#### April, 22

> Logtalk 2.24.0 is now available for [downloading](download.html). This
> release improves the compiler portability reports and the
> \"benchmarks\" example, fixes some bugs related to automatic
> generation and processing of XML documenting files, adds a new
> experimental `encoding/1` directive for declaring the text character
> encoding of a source file and new `info/1-2` documenting directive
> keys for representing predicate call examples, entity parameter
> descriptions, predicate argument descriptions, and general remarks
> about an entity. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### March, 7

> Logtalk 2.23.1 is now available for [downloading](download.html). This
> is a maintenance release featuring some performance improvements, some
> bug fixes, and usability improvements. In addition, the \"benchmarks\"
> example as been updated for testing performance of dynamic code when
> using the built-in database methods. For details, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 21

> Logtalk 2.23.0 is now available for [downloading](download.html),
> featuring a significant performance improvement for applications which
> use an object\'s dynamic database via the database built-in methods
> `clause/2`, `asserta/1`, `assertz/1`, `retract/1`, and `retractall/1`,
> some bug fixes, and usability improvements. For details, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### February, 13

> The beta version of Logtalk 2.22.6 is now available from the
> [CVS](cvs.html) server, featuring a significant performance
> improvement for applications which use an object\'s dynamic database
> via the database built-in methods `clause/2`, `asserta/1`,
> `assertz/1`, `retract/1`, and `retractall/1`.

#### February, 9

> Logtalk 2.22.5 is now available for [downloading](download.html). This
> release improves support for K-Prolog and JIProlog, simplifies and
> improves performance for both the Logtalk compiler and runtime, fixes
> a performance bug with the compilation of built-in predicates, and
> includes several documentation updates. Upgrading to this version is
> recommended to all users. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### January, 13

> An updated config file for K-Prolog is now available for
> [downloading](download.html#updates). This updated file corrects a
> show-stopper bug and contains new predicate definitions which allows
> the use of the \"library\" notation for loading source files (if
> you\'re using Windows, the definition must be edited; see the comments
> on the config file itself).

#### January, 12

> Logtalk 2.22.4 is now available for [downloading](download.html). This
> release simplifies and improves the performance of the method lookup
> caching mechanism, specially for parametric objects, includes a new
> example on using [assignable
> variables](http://www.kprolog.com/en/logical_assignment/) with
> parametric objects, and fixes some minor bugs. For details, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

### 2004

#### December, 30

> Logtalk 2.22.3 is now available for [downloading](download.html). This
> release includes a new configuration file for XSB 2.7 and corrects
> some bugs with the `altdirs` and `debug` compiler options and with the
> built-in debugger. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).
>
> A new web page with Logtalk benchmark results for some Prolog
> compilers is now [available](performance.html).

#### December, 24

> Logtalk 2.22.2 is now available for [downloading](download.html). This
> release provides several performance, compiler, and documentation
> improvements. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).
>
> A new web page with Logtalk benchmark results for some Prolog
> compilers is now [available](performance.html).

#### December, 6

> Logtalk 2.22.1 is now available for [downloading](download.html). This
> release includes a workaround for a Windows Scripting Host bug which
> affects the JScript installer script, improves installation
> instructions and scripts, and provides several usability enhancements
> (particularly for Windows users). For details, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 29

> Logtalk 2.22.0 is now available for [downloading](download.html). This
> release introduces a notion of *library* as a directory of source
> files, adds a dynamic predicate for declaring library names and paths,
> allows source files to be compiled and loaded using the notation
> `<library>(<entity>)`, improves installation instructions and scripts,
> and provides several usability enhancements. For details, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 15

> Logtalk 2.21.6 is now available for [downloading](download.html). This
> release provides usability improvements. For details, please consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### November, 2

> Logtalk 2.21.5 is now available for [downloading](download.html). This
> release focus on performance improvements and enhanced benchmark code.
> For details, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 26

> Logtalk 2.21.4 is now available for [downloading](download.html). This
> release fixes a silly bug on the definition of the predicate
> `repeat/1` used on the new \"benchmarks\" example and tests. For
> details, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 25

> Logtalk 2.21.3 is now available for [downloading](download.html). This
> release provides a small message sending performance improvement, adds
> a new \"benchmarks\" example and a new manual section on message
> sending performance, and improves the usability of some of the
> provided shell scripts. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### October, 18

> Logtalk 2.21.2 is now available for [downloading](download.html). This
> release adds a new `alias/1` predicate property, allows grammar rule
> non-terminals to be used in most predicate directives using the
> notation Functor//Arity, provides a configuration file for JIProlog
> 3.0, and includes support for the new TextMate MacOS X text editor.
> For details, please consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 27

> Logtalk 2.21.1 is now available for [downloading](download.html). This
> release provides several improvements to the Logtalk grammar rule
> translator and some bug fixes. For details, please consult the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 14

> Logtalk 2.21.0 is now available for [downloading](download.html). This
> release adds a new predicate directive, `alias/3`, which allows the
> definition of alternative predicate names in order to improve
> readability of inherited features and to solve conflicts between
> implemented, imported, or inherited predicates. In addition,
> categories are now allowed to import other categories, useful when a
> modified version of a category is needed for importing into several
> unrelated objects. Three new examples are included, illustrating the
> new features of this release. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### September, 4

> An updated syntax mode for the SubEthaEdit 2.x text editor is now
> available from the [download page](download.html#updates). This update
> adds auto-complete strings for Logtalk methods and for Logtalk and
> Prolog built-in predicates.

#### August, 31

> Logtalk 2.20.2 is now available for [downloading](download.html). This
> release adds a Windows JScript install script, improves the Windows
> JScript scripts used for easy integration of Logtalk with selected
> Prolog compilers, and improves the user manual sections on compiler
> options and on defining and using metapredicates. For details, please
> consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

> An article on Logtalk is included on the August issue of the [ALP
> newsletter](http://www.cs.kuleuven.ac.be/~dtai/projects/ALP/newsletter/index.html).

#### August, 19

> Logtalk 2.20.1 is now available for [downloading](download.html). This
> release replaces the Windows JScript scripts lgt2pdf.js and
> lgt2html.js by their correct versions (the wrong ones shipped with
> Logtalk version 2.20.0), adds new Windows JScript scripts for
> automating loading of Logtalk with CIAO and GNU Prolog, fixes a small
> bug in some XSL files with some XSLT processors, and updates the
> \"errors\" example to cover possible errors when using the new
> `uses/2` directive. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 16

> Logtalk 2.20.0 is now available for [downloading](download.html). This
> release adds a new `uses/2` predicate directive, improves installation
> instructions for Windows users, adds new Windows JScript scripts for
> automating loading of Logtalk with selected Prolog compilers, and
> contains new, improved scripts for converting XML documenting files to
> PDF files and (X)HTML files. For details, please consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### August, 2

> Logtalk 2.19.1 is available for [downloading](download.html). This is
> a bug-fix release. For details, consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July, 26

> Logtalk 2.19.0 is available for [downloading](download.html). This
> version features support for defining several entities in the same
> source file, as requested by several users, using *source metafiles*.
> For details, consult the User Manual section on [Logtalk
> programming](manuals/userman/programming.html#source_metafiles) and
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md).

#### July, 19

> A beta version of Logtalk 2.19.0 is available via [CVS](cvs.html),
> featuring support for defining several entities in the same source
> file, as requested by several users. For details, consult the User
> Manual section on Logtalk programming. Your feedback is appreciated.

#### July, 9

> Logtalk 2.18.0 is available for [downloading](download.html). This
> version features several optimizations, including caching of method
> lookups, greatly improving performance. Consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### June, 14

> Logtalk 2.17.2 is available for [downloading](download.html). This
> version improves documentation for first time users, includes a new
> programming example, corrects some bugs related to operator handling
> and local dynamic predicates, updates the compiler to allow source
> files containing only directives, and replaces the examples Prolog
> loader utility files by Logtalk files, thus simplifying example
> loading for new users. Consult the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
> for details.

#### June, 7

> Logtalk 2.17.1 is available for [downloading](download.html). This
> version features new programming examples, provides support for
> documenting exceptions in info/2 directives, fixes a compilation
> problem with B-Prolog, adds a mode bundle for the new SubEthaEdit 2.x
> (MacOS X) text editor, and more. Consult the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### April, 26

> Logtalk 2.17.0 is available for [downloading](download.html). This
> version features a built-in debugger similar to those found on most
> Prolog compilers and a set of shell scripts for Logtalk packaging,
> installation, and integration with selected Prolog compilers. Consult
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### April, 13

> A beta version of Logtalk 2.17.0 is available via [CVS](cvs.html),
> featuring a built-in debugger implemented as a pseudo-object. This
> built-in debugger provides features similar to those found on most
> Prolog compilers. For details, please consult the debugging section on
> the user manual. Your feedback is appreciated.

#### April, 2

> Logtalk 2.16.2 is now available for [download](download.html). This
> version corrects a bug on the library category `monitor` (file
> `library/monitor.lgt`) that prevents its compilation and changes the
> possible values for the read-only compiler option `startup_message`.
> See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### March, 31

> A bug was found on the library category `monitor` (file
> `library/monitor.lgt`) that prevents its compilation. You may download
> an updated version of the category from this
> [page](download.html#updates).

#### March, 22

> Logtalk 2.16.1 is now available for [download](download.html). This
> version allows the local built-in method `parameter/2` to be used
> inside categories, corrects a bug in the compilation of metacalls
> whose meta-arguments are variables, updates the scripts for converting
> XML documenting files into (X)HTML, and improves syntax coloring for
> the SubEthaEdit text editor. See the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### March, 3

> Logtalk 2.16.0 is now available for [download](download.html). This
> version improves support for the declaration and use of operators
> inside objects and categories and for calls to non-standard
> metapredicates from object and categories. In addition, there is a new
> config file for [Qu-Prolog
> 6.4](http://www.itee.uq.edu.au/~pjr/HomePages/QuPrologHome.html). See
> the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### February, 17

> A beta version of Logtalk 2.16.0 is available via [CVS](cvs.html),
> featuring improved support for operators declared inside objects and
> categories. Namely, operators are now local to the objects (or
> categories) declaring them (as required by the Logtalk
> specification!). In addition, the built-in predicates for input and
> output of terms are now aware of local operators. A new example named
> \"operators\" and a new configuration file for [Qu-Prolog
> 6.3](http://www.itee.uq.edu.au/~pjr/HomePages/QuPrologHome.html) are
> also included.

#### February, 16

> Anonymous access to the Logtalk [CVS server](cvs.html) restored.

#### February, 9

> Logtalk 2.15.6 is now available for [download](download.html). This
> version provides significant improvements for the syntax coloring
> configuration files for all supported text editors, including new
> support for the KDE Kate and Kwrite editors. In addition, there is a
> new compiler option related to the automatic generation of XML
> documenting files, new support for the MacOS X Xcode IDE, and two
> small bug fixes. See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for
> details.

### 2003

#### December, 30

> Logtalk 2.15.5 is now available for [download](download.html). This
> version includes a font-lock file for editing Logtalk source files
> with Emacs and updates the documentation to comply with XHTML 1.0
> Strict. See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### October, 19

> A Ph.D. thesis on Logtalk design and implementation is now available
> for [download](documentation.html) (PDF, formatted for A4 paper).

#### July, 9

> Logtalk 2.15.4 is now available for [download](download.html). This
> version improves the experimental support for DCG rules. See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### June, 10

> Logtalk 2.15.3 is now available for [download](download.html). This
> version improves the experimental support for DCG rules. See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### April, 2

> Logtalk 2.15.2 is now available for [download](download.html). This
> version features experimental support for DCG rules. See the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### March, 20

> A beta of the next Logtalk version featuring support for DCG rules
> inside objects and categories is now available from the [CVS
> server](cvs.html).
>
> An updated version of the GNU Prolog configuration file is now
> available from the download [page](download.html).

#### March, 8

> Logtalk 2.15.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### February, 5

> Logtalk 2.15.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### January, 10

> Logtalk 2.14.7 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.
>
> Update config file for CIAO 1.8 is now available for
> [download](download.html#updates).
>
> A first draft of the Logtalk web site RSS feed is now available. The
> URL of the RDF file is: http://www.logtalk.org/logtalk.rdf.

### 2002

#### December, 31

> Logtalk 2.14.6 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### December, 20

> Logtalk 2.14.5 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### November, 5

> Logtalk 2.14.4 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### September, 16

> Logtalk 2.14.3 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### August, 26

> Logtalk 2.14.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### August, 3

> The documentation of the Logtalk standard library is now available
> [on-line](documentation.html).

#### July, 31

> Logtalk 2.14.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### July, 26

> Logtalk 2.14.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### June, 15

> Logtalk 2.13.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### May, 25

> Logtalk 2.12.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### May, 21

> A NEdit 5.2 syntax patterns file for Logtalk is now available for
> downloading from <http://www.logtalk.org/files/nedit/logtalk.pats>.
> NEdit is a multi-purpose text editor for the X Window System that
> features syntax highlighting for many programming languages. The
> Logtalk syntax patterns file provides syntax highlight for Logtalk
> source files.

#### May, 17

> The new Logtalk domain name, `logtalk.org`, is now active. The Logtalk
> web site can now be accessed using the URL <http://www.logtalk.org/>.
> The Logtalk CVS server can be accessed from `cvs.logtalk.org`.

> A VIM 6.1 syntax file for Logtalk is now available for downloading
> from <http://www.logtalk.org/files/vim/logtalk.vim>. VIM is greatly
> improved version of the VI text editor that features syntax
> highlighting for many programming languages. The editor runs in most
> platforms. The Logtalk syntax file provides syntax highlight for
> Logtalk source files.

#### May, 6

> A jEdit 4.0 edit mode file for Logtalk is now available for
> downloading from <http://community.jedit.org/>. jEdit is an open
> source text editor that features syntax highlighting for many
> programming languages. The editor is written in Java, running in most
> platforms. The Logtalk edit mode file provides syntax highlight for
> Logtalk source files.

#### April, 29

> An updated configuration file for OpenProlog 1.1b5 is now available
> for [downloading](download.html).

#### April, 24

> Logtalk 2.11.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### April, 5

> Logtalk 2.10.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### February, 9

> Logtalk 2.9.3 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.
>
> All Logtalk site web pages have been converted to [XHTML
> 1.0](http://www.w3.org/MarkUp/) format. Also, the images at the bottom
> of the pages are converted to [PNG](http://www.libpng.org/) format.

#### January, 4

> Logtalk 2.9.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

### 2001

#### December, 13

> A new version of the Logtalk compiler is available from the
> [download](download.html) page fixing a bug in the updating of the
> entity relation tables when an entity is loaded. See the [bugs and
> known issues](bugs.html) page for details.

#### December, 5

> Logtalk 2.9.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### October, 30

> An experimental CVS server is now available from the [CVS](cvs.html)
> page providing access to the latest Logtalk source files.

#### October, 29

> A new version of the Logtalk compiler is available from the
> [download](download.html) page fixing a bug in the error checking code
> of directives `info/1` and `info/2`. See the [bugs and known
> issues](bugs.html) page for details.

#### October, 22

> Logtalk 2.9.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### August, 21

> New configuration files for B-Prolog 6.0 and CIAO Prolog 1.7p115 are
> now available for [downloading](download.html).

#### June, 28

> Logtalk 2.8.4 is now included with the
> [YAP](http://www.cos.ufrj.br/~vitor/Yap/) Prolog compiler.

#### March, 9

> Logtalk 2.8.4 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### February 6

> Updated configuration files for K-Prolog 5.0.1 and BinProlog 8.0 are
> now available for [downloading](download.html).

### 2000

#### November, 21

> Logtalk 2.8.3 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### November, 5

> Logtalk 2.8.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### October, 28

> Logtalk 2.8.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### October, 1

> Logtalk 2.8.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### August, 24

> Logtalk 2.7.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.

#### July, 11

> A preliminary config file for CIAO 1.5pl169 is now available for
> [download](download.html).

#### July, 4

> Logtalk 2.6.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) for details.
>
> New updated versions of all documentation are now available for
> [download](download.html). The PDF versions, available in both A4 and
> US Letter formats, now contain page numbers, index, and a table of
> contents. The HTML version is fully synchronized with the PDF
> versions.

#### May, 14

> An updated config file for Bin Prolog 7.83 is now available for
> [download](download.html). Updated link to XSB home page.

#### May, 5

> Logtalk 2.6.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### April, 27

> Logtalk 2.6.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### April, 24

> Logtalk 2.6.0 beta 2 is now available for download for registered
> users, improving the automatic generation of documentation files in
> XML format.

#### April, 20

> Logtalk 2.6.0 beta 1 is now available for download for registered
> users. Major new feature is the automatic generation of documentation
> files in XML format.

#### March, 29

> Updated all web pages to comply with the HTML 4.01 strict standard.

#### March, 7

> Logtalk 2.5.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### February, 18

> Logtalk 2.5.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

### 1999

#### December, 29

> Logtalk 2.5.0 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### December, 1

> Logtalk 2.4.0 is now available for [download](download.html). Logtalk
> is now an [Open Source](http://www.opensource.org/) project available
> under the [Perl Artistic license](license.html). See the [release
> notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### September, 22

> A new config file for GNU Prolog 1.0.6 (or later version) is now
> available for [download](download.html). This config file uses a new
> GNU Prolog built-in predicate for better performance.

#### September, 22

> Logtalk 2.3.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### September, 21

> New [related links](links.html) page.

#### September, 19

> The registration, bug and support forms should work now (I have
> switched the form action to send the form contents by email). Sorry
> for the inconvenience.

#### September, 12

> Logtalk 2.3 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### July, 15

> Logtalk 2.2 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### June, 3

> Updated config files for some Prolog compilers are available from the
> [download](download.html) page. See the [known problems and bugs
> list](bugs.html) for details.

#### May, 11

> Logtalk 2.1 is now available for [download](download.html). See the
> [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md) page for details.

#### April, 14

> A bug in the definition of the pseudo-object `user` have been found.
> See the [bugs](bugs.html) page for details.

#### February, 10

> The final release of Logtalk 2.0 is now available for
> [download](download.html). See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
> for details.

#### February, 1

> Third public beta release of Logtalk 2.0 is now available for
> [download](download.html). See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
> for details.

### 1998

#### December, 13

> An updated config file for Amzi Prolog is now available for
> [download](download.html). See the [known bugs list](bugs.html) for
> details.

#### November, 16

> Second public beta release of Logtalk 2.0 is now available for
> [download](download.html). See the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
> for details.

#### October, 21

> Corrected broken links to the [tutorial](manuals/tutorial/index.html)
> pages.

> Updated the manual pages describing [error
> handling](manuals/userman/errors.html) to match the latest changes in
> the Logtalk pre-processor.

> Updated the [known problems and bugs](bugs.html) page.

#### October, 18

> First public beta release of Logtalk 2.0 now available for
> [download](download.html).

> Removed all references to previous, 1.x, Logtalk versions from this
> web server (they can still be obtained by email request).

#### September, 10

> New alpha seed of [Logtalk 2.0](manuals/index.html) now available with
> support for multi-inheritance.

#### August, 14

> The current drafts of the User and Reference Manuals of Logtalk 2.0
> can be browsed [here](manuals/index.html).

#### July, 8

> An alpha version of [Logtalk 2.0](manuals/index.html) is now available
> by [email request](supportform.html) for [registered
> users](support.html#registration).

#### January

> Development of Logtalk 2.0 begins.
