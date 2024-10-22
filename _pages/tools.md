---
layout: article
permalink: tools.html
title: Tools
aside:
  toc: true
---

Logtalk includes a comprehensive set of developer tools allows you to write,
debug, profile, document, diagram, and test your code. Most of the tools are
implemented as Logtalk applications using the
[reflection API](manuals/userman/reflection.html). This API can be used to
implement alternative tools or new tools. Follows an overview of each tool
and some usage examples.

## Learning

The [`tutor`](https://logtalk.org/manuals/devtools/tutor.html) tool
helps new users understand the compiler and runtime warning and error messages
by adding explanations and suggestions to selected messages. Usage simply requires
loading the tool at startup. As an example, with this tool loaded, instead of
terse compiler warnings such as:

```text
*     No matching clause for goal: baz(a)
*       while compiling object main_include_compiler_warning
*       in file /Users/pmoura/logtalk/examples/errors/include_compiler_warning.lgt between lines 37-38
*     
*     Duplicated clause: b(one)
*       first found at or above line 45
*       while compiling object main_include_compiler_warning
*       in file /Users/pmoura/logtalk/examples/errors/include_compiler_warning.lgt at or above line 48
```

the user will get:

```text
*     No matching clause for goal: baz(a)
*       while compiling object main_include_compiler_warning
*       in file /Users/pmoura/logtalk/examples/errors/include_compiler_warning.lgt between lines 37-38
*     Calls to locally defined predicates without a clause with a matching head
*     fail. Typo in a predicate argument? Predicate definition incomplete?
*     
*     Duplicated clause: b(one)
*       first found at or above line 45
*       while compiling object main_include_compiler_warning
*       in file /Users/pmoura/logtalk/examples/errors/include_compiler_warning.lgt at or above line 48
*     Duplicated clauses are usually a source code editing error and can
*     result in spurious choice-points, degrading performance. Delete or
*     correct the duplicated clause to fix this warning.
```

There's also a [`help`](https://logtalk.org/manuals/devtools/help.html) tool
that provides quick access to Logtalk documentation. In particular, with most
backend Prolog systems, this tool supports browsing and searching the Texinfo
versions of the Handbook and APIs documentation inline at the top-level.


## Lint checker

Although not technically a developer tool, it is worth mentioning the Logtalk
extensive compiler lint checks as they contribute to earlier detection and
warning of source code issues, helping the user in writing clean and efficient
working code that also comply with coding guidelines. Lint checks include:

-   Missing directives (including scope, meta-predicate, dynamic, discontiguous, and multifile directives)
-   Duplicated directives, clauses, and grammar rules
-   Missing predicates (unknown messages plus calls to non-declared and non-defined predicates)
-   Calls to declared but not defined static predicates
-   Non-terminals called as predicates (instead of via the `phrase/2-3` built-in methods)
-   Predicates called as non-terminals (instead of via the `call//1` built-in method)
-   Non-portable predicate calls, predicate options, arithmetic function calls, directives, flags, and flag values
-   Missing arithmetic functions (with selected backends)
-   Suspicious calls (syntactically valid calls that are likely semantic errors; e.g. float comparisons using the standard arithmetic comparison operators or comparing numbers using unification)
-   Deprecated directives, predicates, control constructs, and flags
-   References to unknown entities (objects, protocols, categories, or modules)
-   Top-level shortcuts used as directives
-   Unification goals that will succeed without binding any variables
-   Unification goals that will succeed creating a cyclic term
-   Goals that are always true or always false
-   Trivial goal fails (due to no matching predicate clause)
-   Redefined built-in predicates
-   Redefined standard operators
-   Lambda expression unclassified variables and mixed up variables
-   Lambda expression with parameter variables used elsewhere in a clause
-   Singleton variables
-   If-then-else and soft cut control constructs without an else part
-   If-then-else and soft cut control constructs where the test is a unification between a variable and a ground term
-   Missing parenthesis around if-then-else and disjunction control constructs in the presence of cuts in the first argument
-   Cuts in clauses for multifile predicates
-   Missing cuts in repeat loops
-   Possible non-steadfast predicate definitions
-   Non-tail recursive predicate definitions
-   Redundant calls to control constructs and built-in predicates
-   Calls to all-solutions predicates with existentially qualified variables not occurring in the qualified goal
-   Calls to all-solutions predicates with no shared variables between template and goal
-   Calls to `bagof/3` and `setof/3` where the goal argument contains singleton variables
-   Calls to `findall/3` used to backtrack over all solutions of a goal without collecting them
-   Calls to `catch/3` that catch all exceptions
-   Calls to standard predicates that have more efficient alternatives
-   Unsound calls in grammar rules
-   File, entity, predicate, and variable names not following official coding guidelines
-   Variable names that differ only on case
-   Clauses whose body is a disjunction (and that can be rewritten as multiple clauses per coding guidelines)
-   Naked meta-variables in cut-transparent control constructs
-   Left-recursion in clauses and grammar rules

Lint checks are controlled by a set of [compiler flags](https://logtalk.org/manuals/userman/programming.html#lint-flags).
Additional checks are provided by the [`lgtunit`](#testing), [`lgtdoc`](#documenting), [`make`](#make), and [`dead_code_scanner`](#dead-code-scanner) tools, by libraries, and by other developer tools. For large projects, the data generated by the [`code_metrics`](#code-metrics) tool may also be relevant in accessing the quality of your code.

Experimental support for extending the linter with user-defined warnings is
available using a multifile hook predicate. For example, the `list` library
object defines this hook predicate to lint calls to the `append/3` predicate
for common misuses.


## Documenting

Logtalk includes two documenting tools, [`lgtdoc`](https://logtalk.org/manuals/devtools/lgtdoc.html)
and [`doclet`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/doclet/NOTES.md), and
[`logtalk_doclet`](man/logtalk_doclet.html) Bash and PowerShell scripts.
The `lgtdoc` tool exports API documentation files in XML format and includes
scripts to convert these files into a final format such as HTML, PDF, or
Markdown. The `doclet` tool can be used to automate the steps to generate
API documentation and diagrams for a Logtalk application.

Logtalk documenting directives allows the programmer to represent
extensive API information on entities and their predicates including:

-   Entity authors, change date, version, description, and general remarks
-   Parametric entity parameter names and descriptions
-   Entity compilation flags
-   Entity user-defined keys
-   Predicate description
-   Predicate argument types, instantiation modes, and number of proofs
-   Predicate exceptions and usage examples
-   Predicate user-defined keys

This information is made available for tools such as `lgtdoc` using the reflection API.

##### Examples

-   API documentation in HTML format of the [`iso8601`](library/iso8601_0.html) library
-   [Core, library, and tools](library/index.html) API documentation in HTML format illustrating the generated indexes


## Diagrams

Diagrams provide a navigable structural view of source code at multiple levels of abstraction.
The [`diagrams`](https://logtalk.org/manuals/devtools/diagrams.html) tool supports:

-   Library loading diagrams
-   Library dependency diagrams
-   Directory loading diagrams
-   Directory dependency diagrams
-   File loading diagrams
-   File dependency diagrams
-   Inheritance diagrams
-   Entity cross-referencing diagrams
-   Predicate cross-referencing diagrams
-   Diagrams with links to source code repositories and API documentation
-   Linked diagrams for source code navigation from libraries to entities to predicates
-   Linked diagrams for source code navigation from directories to files
-	Automatic generation of linked sub-diagrams
-   Diagrams represented in Graphviz dot language
-   Exporting of diagrams to SVG, PDF, and other formats
-	Diagram exporting automation scripts (for use with e.g. the [`doclet`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/doclet/NOTES.md) tool)
-   User customization of diagram details
-	Support for generating diagrams for module applications when using selected Prolog systems

##### Examples

Linked diagrams with live URLs to code and documentation (click on the nodes, labels, zoom icons, and directory and file names to navigate):

-	[Logtalk `ports_profiler` object cross-referencing diagram](docs/ports_profiler_object_xref_diagram.svg)
-   [Logtalk developer `tools` library diagram](library/tools_inheritance_diagram.svg)
-   [Logtalk developer `tools` directory diagram](diagrams/tools/tools_directory_load_diagram.svg)
-   [SWI-Prolog Talespin application entity diagram](diagrams/talespin/talespin_entity_diagram.svg)
-   [SWI-Prolog ClioPatria application directory diagram](diagrams/cliopatria/cliopatria_directory_load_diagram.svg)


## Testing

The [`lgtunit`](https://logtalk.org/manuals/devtools/lgtunit.html) testing tool
can be used to test both Logtalk and Prolog code and provides an extensive set of features including:

-   Multiple test dialects
-   User-defined test dialects
-   QuickCheck support (for property-based testing)
-   Code coverage reports (at the predicate clause level; supports links to selected source code hosting providers)
-   Test assertions (for easier debugging of failed tests)
-   Support for testing input/output predicates
-   Support for suppressing irrelevant text/binary output by the code under testing
-   Predicate determinism testing
-   Benchmarking support
-   Approximate float comparison support
-   Test set and per test annotations
-   Parametrized unit tests
-   Testing automation scripts (supports CI/CD pipelines with detailed test and code coverage reports)
-   TAP and xUnit test reports
-   Test set condition, setup, and cleanup goals
-   Per test condition, setup, and cleanup goals
-   Flaky tests marking and reporting
-   Support for test subsets (with generation of a single code coverage report)
-   Make tool integration

QuickCheck support includes both test idioms and predicates that can be used e.g. at the top-level for quick testing of plain Prolog predicates and Prolog modules predicates besides Logtalk object predicates.

Test automation is provided by the [`logtalk_tester`](man/logtalk_tester.html) Bash and PowerShell scripts.
See also the [testing guide](testing.html) and the [blog posts](blog.html?tag=testing)
on testing best practices for more information. Automatic bug report creation for failed
tests in GitHub and GitLab issue trackers is supported using the
[`issue_creator`](https://logtalk.org/manuals/devtools/issue_creator.html) tool.

##### Examples

-   [Code coverage report](diagrams/coverage_report.html) for the [`diagrams`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/diagrams/NOTES.md) tool
-   [Prolog standards conformance suite](https://github.com/LogtalkDotOrg/logtalk3/tree/master/tests/prolog)
-   Prolog standards conformance suite [results for GNU Prolog 1.5.1](https://logtalk.org/files/allure-report/)


## Dead code scanner

The [`dead_code_scanner`](https://logtalk.org/manuals/devtools/dead_code_scanner.html)
tool detects likely dead code in Logtalk entities and in Prolog modules (when compiled as objects). It can also
detect code typos that often result in false positives. It can be run automatically was one of the actions of
the [`make`](#make) tool.


## Code metrics

The [`code_metrics`](https://logtalk.org/manuals/devtools/code_metrics.html)
tool allows applying code metrics to source code. Several basic metrics are provided:

-   Halstead complexity
-   Cyclomatic complexity
-   Efferent coupling
-   Afferent coupling
-   Instability
-   Abstractness
-   Documentation
-   Source code size
-   Depth of Inheritance
-   Number of Clauses
-   Number of Rules

The tool is extensible allowing users to define their own metrics.


## Ports profiler

The [`ports_profiler`](https://logtalk.org/manuals/devtools/ports_profiler.html)
tool is a code profiling tool based on the extended procedure
box model (using the same reflection API as the [`debugger`](#debugging) tool) to count and
report the number of times each port is traversed during the execution of
queries. It provides valuable insight on predicate usage allowing e.g. the
detection of problems that can cause poor performance.


## Debugging

Logtalk provides an extended procedure box model that supports:

-   Classic call, exit, redo, and fail ports
-   Exception port
-   Fact and rule unification ports

This procedure box model is leveraged by the [`debugger`](https://logtalk.org/manuals/devtools/debugger.html)
tool to provide:

-   Traditional predicate breakpoints
-   Context breakpoints
-   Clause breakpoints (at unification ports)
-	Conditional breakpoints (at unification ports)
-	Hit count breakpoints (at unification ports)
-	Triggered breakpoints (at unification ports)
-	Log points (at unification ports) with templated messages
-   Extended set of debugging commands at leashed ports

Another debugging tool, [`debug_messages`](https://logtalk.org/manuals/devtools/debug_messages.html),
allows selectively enabling of debug messages. Related, the Logtalk message printing mechanism supports a set of predefined
[meta messages](library/logtalk_0.html#remarks) that are handy for debugging.

Logtalk also provides a [debugging control construct](manuals/refman/control/context_switch_2.html) for calling and testing local object predicates.

See the Handbook section on [debugging](manuals/userman/programming.html#programming_debugging) for more details.


## Make

Logtalk supports extended [`make`](https://logtalk.org/manuals/devtools/make.html) functionality:

-   Reloading of modified files
-   Cleaning of the intermediate Prolog files generated by the compiler
-   Generating documentation
-   Listing of missing entities
-   Listing of missing predicates
-   Listing of circular entity dependencies
-	Listing of duplicated library aliases
-   Recompilation of loaded files in a different mode (e.g. debug mode)
-   User-defined make actions (e.g. running unit tests automatically when reloading modified files)
-   Cleaning of the dynamic binding caches

The top-level interpreter supports handy [shortcuts](manuals/refman/predicates/logtalk_make_1.html)
for all the `make` features.


## Package manager

Logtalk provides a [`packs`](https://logtalk.org/manuals/devtools/packs.html)
for installing third-party libraries and applications. This is a portable tool that supports multiple
registries (e.g. official, public, company private, ...) and allows user to:

-	Create and publish their own pack registries
-	Publish packs verified by checksums and optionally signed and encrypted
-	Add, pin, update, and delete pack registries
-	Install, pin, update, and uninstall packs
-	List available, installed, outdated, orphaned, and dependent packs
-	Define registries as git repos, archives, or local directories
-	Specify multiple pack versions
-	Work with minimal specifications for registries and packs
-	Define, save, and restore virtual environments (registries/packs setups)

There's also an [index](https://github.com/LogtalkDotOrg/pack-registries) of public pack registries.
This tool can be used not only for Logtalk packs but also for Prolog packs.


## Literate programming

A [Jupyter kernel for Logtalk](https://github.com/LogtalkDotOrg/logtalk-jupyter-kernel)
is available that can be used with a subset of the Logtalk supported Prolog backends.
The latest release can be installed from [PyPI](https://pypi.org/project/logtalk-jupyter-kernel/)
or [Conda](https://anaconda.org/conda-forge/logtalk-jupyter-kernel).

There's also a [Docker image](https://hub.docker.com/r/logtalk/logtalk3-portable)
with Logtalk, selected Prolog backends, and Jupyter pre-installed.


## Prolog porting

The [`wrapper`](https://logtalk.org/manuals/devtools/wrapper.html)
tool can be used to help port a plain Prolog application to Logtalk by analyzing its source
files and suggesting object wrappers and their public interfaces. It can also be used to enable
applying other Logtalk developer tools, such as the documenting and diagramming tools, to plain
Prolog code. See also the guide on
[applying Logtalk tools to Prolog codebases](using_tools_with_prolog.html), which can be used
to gain additional insight on the changes required when porting applications.


## Coding

The Logtalk distribution includes [extensive](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding)
support for text editors, syntax highlighters (for publishing code), and several IDEs. The VSCode extension
available from the [VSCode](https://marketplace.visualstudio.com/items?itemName=LogtalkDotOrg.logtalk-for-vscode)
and [VSCodium](https://open-vsx.org/extension/LogtalkDotOrg/logtalk-for-vscode) marketplaces is recommended.
For convenience, there's also a VSCode extension pack that installs all recommended extensions for Logtalk development
available from the [VSCode](https://marketplace.visualstudio.com/items?itemName=LogtalkDotOrg.logtalk-extension-pack)
and [VSCodium](https://open-vsx.org/extension/LogtalkDotOrg/logtalk-extension-pack) marketplaces.


## Embedding

Logtalk includes a set of sample [helper scripts](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/embedding)
with [usage examples](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/embedding/SCRIPT.txt)
for embedding the Logtalk runtime and Logtalk applications using selected backend Prolog compilers. These scripts greatly
simplify packaging and delivering of applications and can be used as basis for e.g. automatically generating executables and JAR files.


## Version management

The Logtalk distribution includes a [`logtalk_version_select`](man/logtalk_version_select.html)
script that allows listing and switching between installed versions.

A [Logtalk plugin](https://github.com/LogtalkDotOrg/asdf-logtalk) for the `asdf` extendable version manager is also available.
This plugin provides an alternative that can be useful to manage Logtalk versions when developing solutions that use other
languages and tools that can also be handled by `asdf`.


## GitHub actions and workflows

GitHub actions and workflows are [available](https://github.com/logtalk-actions) for CI/CD of Logtalk applications with source code repos hosted at GitHub. See the [demo](https://github.com/logtalk-actions/demo) repo for an example of automating testing with xUnit and code coverage reports, (re)generating API documentation, and (re)generating application diagrams every time a commit is made.


## Project scaffolding

The following tools are not part of the Logtalk distribution but kindly contributed by Logtalk users:

### Cookiecutter Logtalk

[Cookiecutter](https://cookiecutter.readthedocs.io/) is a Python tool that creates projects from project templates. It supports project templates that can be in any programming language or markup format, now including Logtalk, thanks to Paul Brown. To install Cookiecutter Logtalk, visit its [GitHub repo](https://github.com/PaulBrownMagic/cookiecutter-logtalk).

### lgtinit

[lgtinit](https://github.com/eazar001/lgtinit) is a POSIX script for project scaffolding contributed by Ebrahim Azarisooreh.


## Third-party tools

### SWI-Prolog tools

Logtalk supports [SWI-Prolog](http://www.swi-prolog.org/) `edit/1`, `make/0`, `consult/1`, and `load_files/2` (to load Logtalk source files) predicates, the graphical profiler, and the graphical tracer. Recent versions of both Logtalk and SWI-Prolog are required. See the `settings-sample.lgt` file for the **required** settings to use the graphical tracer and the graphical profiler.

### YAP profilers

Logtalk supports the [YAP](http://www.cos.ufrj.br/~vitor/Yap/) tick and count profilers. See the `profiler` tool in the current Logtalk distribution for details.

### SICStus Prolog profilers

Logtalk supports the [SICStus Prolog 4](http://www.sics.se/isl/sicstus.html) profiler. See the `profiler` tool in the current Logtalk distribution for details.

### PDT

[PDT](https://sewiki.iai.uni-bonn.de/research/pdt/docs/start) is an open source Prolog IDE provided as a plug-in for the Eclipse IDE. PDT is being extended with Logtalk support.

PDT currently requires a recent version of SWI-Prolog. It's possible to start up Logtalk automatically by configuring PDT runtime preferences. The configuration depends on the operating-system. After installing Logtalk and setting the `LOGTALKHOME` and `LOGTALKUSER` environment variables, open Eclipse preferences, select PDT runtime preferences, and enter the following configuration data for the SWI-Prolog executable and for the extra environment variables (change the paths to match your SWI-Prolog and Logtalk installations and your home directory; also, restart Eclipse after entering and saving the configuration data):

##### macOS example configuration

	/Users/pmoura/bin/swipl -s /opt/local/share/logtalk/integration/logtalk_swi.pl
	DISPLAY=:0.0, HOME=/Users/pmoura, LOGTALKHOME=/opt/local/share/logtalk, LOGTALKUSER=/Users/pmoura/logtalk

Notes: full paths should be used; no quotes should be used.

##### Windows example configuration

	cmd.exe /c start "cmdwindow" /min "C:\Program Files\pl\bin\swipl-win.exe" -f "%LOGTALKHOME%\integration\logtalk_swi.pl"

Notes: if you're using a recent SWI-Prolog development version you may use the `-s` option instead of `-f`.

##### Linux example configuration

	/usr/bin/swipl -L4m -G4m -T4m -s /usr/share/logtalk/integration/logtalk_swi.pl
	LOGTALKHOME=/usr/share/logtalk, LOGTALKUSER=/home/pmoura/logtalk

Notes: full paths should be used; no quotes should be used.

Using PDT also **requires** specific Logtalk settings. The [`settings-sample.lgt`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/settings-sample.lgt) file includes two sets of settings for PDT: a basic one and an extended one for allowing use of the SWI-Prolog graphical debugger for tracing Logtalk code. See the comments in the file on how to use settings files.

Currently supported PDT features include consulting Logtalk source files, the source file outline (which requires the source code to be consulted first), and selecting a goal and searching for all declarations and definitions (you must select the whole goal and control-click on the selection).

### Source code version control systems

The [coding](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding)
directory includes sample *ignore files* for common source code version
control systems such as Git and Mercurial.

### Source code stats

[`cloc`](https://github.com/AlDanial/cloc),
[`ohcount`](https://github.com/blackducksoftware/ohcount), and
[`tokei`](https://github.com/Aaronepower/tokei) are open-source command-line
tools that count blank lines, comment lines, and lines of source code in
many programming languages including Logtalk.

### macOS QuickLook

macOS supports previewing files without opening them using a feature named QuickLook. By default, quick looking a file is just a question of selecting it in the Finder and pressing the keyboard's space bar. To make this feature also work for previewing Logtalk source files, you can add the necessary registry information to a text editor such as TextMate 2 by editing the application `Info.plist` file and adding the following lines to the `UTImportedTypeDeclarations` section:

	{
		UTTypeIdentifier   = "org.logtalk";
		UTTypeTagSpecification = {
			public.filename-extension = ( lgt, logtalk );
		};
		UTTypeConformsTo   = ( "public.source-code" );
		UTTypeIconFile     = "Logtalk";
		UTTypeDescription  = "Logtalk source";
		UTTypeReferenceURL = "https://logtalk.org";
	},

If the `Info.plist` is using XML syntax, then use instead:

```xml
<dict>
	<key>UTTypeConformsTo</key>
	<array>
		<string>public.source-code</string>
	</array>
	<key>UTTypeDescription</key>
	<string>Logtalk source</string>
	<key>UTTypeIconFile</key>
	<string>Logtalk</string>
	<key>UTTypeIdentifier</key>
	<string>org.logtalk</string>
	<key>UTTypeReferenceURL</key>
	<string>https://logtalk.org</string>
	<key>UTTypeTagSpecification</key>
	<dict>
		<key>public.filename-extension</key>
		<array>
			<string>lgt</string>
			<string>logtalk</string>
		</array>
	</dict>
</dict>
```

After saving the `Info.plist` file, close TextMate if open and re-open it. Then try to QuickLook a Logtalk source file. You should get a preview window with nice syntax highlighting for your code. If not, move the TextMate application to a different folder (e.g. you Desktop) and then back to its original location. This is usually enough to get the Finder to notice and register the Quick Look changes in the application bundle.
