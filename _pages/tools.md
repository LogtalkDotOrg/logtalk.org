---
layout: article
permalink: tools.html
title: Tools
aside:
  toc: true
---

Logtalk includes a comprehensive set of developer tools allows you to write,
debug, profile, document, diagram, and test your code. Most of the tools are
implemented as Logtalk applications using the reflection API. This API can be
used to implement alternative tools or new tools. Follows an overview of each
tool and some usage examples.

## Lint checker

Although not technically a developer tool, it is worth mentioning the Logtalk
compiler lint checks as they contribute to earlier detection and warning of
source code issues. Lint checks include:

-   Missing directives (including scope, meta-predicate, dynamic, discontiguous, and multifile directives)
-   Duplicated directives
-   Missing predicates (calls to non-declared and non-defined predicates)
-   Calls to declared but not defined static predicates
-   Non-portable predicate calls, arithmetic function calls, directives, flags, and flag values
-   Suspicious calls (syntactically valid calls that are likely semantic errors)
-   Deprecated directives, control constructs, and flags
-   References to unknown entities (objects, protocols, categories, or modules)
-   Goals that are always true or always false
-   Trivial goal fails (due to no matching predicate clause)
-   Redefined built-in predicates
-   Lambda expression unclassified variables and mixed up variables
-   Singleton variables

Additional checks are provided by the [`make`](#make) and [`dead_code_scanner`](#dead-code-scanner) tools.


## Documenting

Logtalk includes two documenting tools, [`lgtdoc`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtdoc/NOTES.md)
and [`doclet`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/doclet/NOTES.md), and an
automation script, [`logtalk_doclet`](man/logtalk_doclet.html). The `lgtdoc` tool exports API
documentation files in XML format and includes scripts to convert
these files into a final format such as HTML, PDF, or Markdown.
The `doclet` tool can be used to automate the steps to generate API
documentation and diagrams for a Logtalk application.

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

The [`diagrams`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/diagrams/NOTES.md) tool supports:

-   Library loading diagrams
-   Library dependency diagrams
-   File loading diagrams
-   File dependency diagrams
-   Inheritance diagrams
-   Entity cross-referencing diagrams
-   Predicate cross-referencing diagrams
-   Diagrams with links to source code repositories and API documentation
-   Linked diagrams for source code navigation from libraries to entities to predicates
-   Diagrams represented in Graphviz dot language
-   Exporting of diagrams to SVG, PDF, and other formats
-   User customization of diagram details

##### Examples

-   [Tools diagram](library/tools_inheritance_diagram.svg) with links to code and documentation
-   [Zoom linked diagrams](diagrams/zoom_example/tools_library_dependency_diagram.svg) of the Logtalk developer tools (click on the zoom icons to navigate)
-   An example of using the diagrams tool with Prolog using the [SWI-Prolog library](diagrams/swi_prolog_library_entity_diagram.svg) (with links to code and documentation): 
-   Another example of using the diagrams tool to generate a [predicate cross-referencing diagram](diagrams/pengines_module_xref_diagram.pdf) for the SWI-Prolog pengines module


## Testing

The [`lgtunit`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md) testing tool
can be used to test both Logtalk and Prolog code and provides an extensive set of features including:

-   Multiple test dialects
-   User-defined test dialects
-   QuickCheck support
-   Code coverage reports (at the predicate clause level; supports links to selected source code hosting providers)
-   Test assertions (for easier debugging of failed tests)
-   Support for testing input/output predicates
-   Support for suppressing irrelevant text/binary output by the code under testing
-   Predicate determinism testing
-   Benchmarking support
-   Approximate float comparison support
-   Test set and per test annotations
-   Parametrized unit tests
-   Testing automation script (supports CI servers)
-   TAP and xUnit test reports
-   Test set condition, setup, and cleanup goals
-   Per test condition, setup, and cleanup goals
-   Support for test subsets (with generation of a single code coverage report)
-   Make tool integration

Test automation is provided by the [`logtalk_tester`](man/logtalk_tester.html) script.
See also the [testing guide](testing.html) for more information.

##### Examples

-   [Code coverage report](diagrams/coverage_report.html) for the diagrams tool
-   [Prolog standards conformance suite](https://github.com/LogtalkDotOrg/logtalk3/tree/master/tests/prolog)


## Dead code scanner

The [`dead_code_scanner`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/dead_code_scanner/NOTES.md)
tool detects likely dead code in Logtalk entities and in Prolog modules (when compiled as objects). It can also
detect code typos that often result in false positives. It can be run automatically was one of the actions of
the [`make`](#make) tool.


## Code metrics

The [`code_metrics`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/code_metrics/NOTES.md)
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

The [`ports_profiler`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/ports_profiler/NOTES.md)
tool is a code profiling tool based on the extended procedure
box model (using the same reflection API as the [`debugger`](#debugging) tool) to count and
report the number of times each port is traversed during the execution of
queries. It provides valuable insight on predicate usage allowing e.g. the
detection of problems that can cause poor performance.

##### Examples

-   Profiling [session](https://forums.logtalk.org/viewtopic.php?f=21&t=240) of the `searching` example sample queries.


## Debugging

Logtalk provides an extended procedure box model that supports:

-   Classic call, exit, redo, fail ports
-   Exception port
-   Fact and rule unification ports

This procedure box model is leveraged by the [`debugger`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/debugger/NOTES.md)
tool to provide:

-   Predicate spy points
-   Context spy points
-   Breakpoints (aka line number spy points)
-   Extended set of debugging commands at leashed ports

Another debugging tool, [`debug_messages`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/debug_messages/NOTES.md).
allows selectively enabling of debug messages. Related, the Logtalk message printing mechanism supports a set of predefined
[meta messages](library/logtalk_0.html#remarks) that are handy for debugging.

Logtalk also provides a [debugging control construct](manuals/refman/control/context_switch_2.html) for calling and testing local object predicates.

See the Handbook section on [debugging](manuals/userman/programming.html#programming_debugging) for more details.

## Make

Logtalk supports extended [`make`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/make/NOTES.md) functionality:

-   Reloading of modified files
-   Cleaning of the intermediate Prolog files generated by the compiler
-   Generating documentation
-   Listing of missing entities
-   Listing of missing predicates
-   Listing of circular entity dependencies
-   Recompilation of loaded files in a different mode (e.g. debug mode)
-   User-defined make actions (e.g. running unit tests automatically when reloading modified files)
-   Cleaning of the dynamic binding caches

The top-level supports handy [shortcuts](manuals/refman/predicates/logtalk_make_1.html)
for all the `make` features.


## Prolog porting

The [`wrapper`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/wrapper/NOTES.md)
tool can be used to help port a plain Prolog application to Logtalk by analyzing its source
files and suggesting object wrappers and their public interfaces. It can also be used to enable
applying other Logtalk developer tools, such as the documenting and diagramming tools, to plain
Prolog code.


## Coding

The Logtalk distribution includes [extensive](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding)
support for text editors, syntax highlighters (for publishing code), and several IDEs.


## Embedding

Logtalk includes a set of [helper scripts](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/embedding)
for embedding the Logtalk runtime and Logtalk applications using selected backend Prolog compilers. These scripts greatly
simplify packaging and delivering of applications and can be used as basis for e.g. automatically generating executables and JAR files.

##### Examples

-   [Embedding examples](https://github.com/LogtalkDotOrg/logtalk3/tree/master/scripts/embedding/SCRIPT.txt)


## Version management

The Logtalk distribution includes a [`logtalk_version_select`](man/logtalk_version_select.html)
script that allows listing and switching between installed versions.

A [Logtalk plugin](https://github.com/LogtalkDotOrg/asdf-logtalk) for the `asdf` extendable version manager is also available.
This plugin provides an alternative that can be useful to manage Logtalk versions when developing solutions that use other
languages and tools that can also be handled by `asdf`.


## Third-party tools

### SWI-Prolog tools

Logtalk supports [SWI-Prolog](http://www.swi-prolog.org/) `edit/1`, `make/0`, `consult/1`, and `load_files/2` (to load Logtalk source files) predicates, the graphical profiler, and the graphical tracer. Recent versions of both Logtalk and SWI-Prolog are required. See the `settings-sample.lgt` file for the **required** settings to use the graphical tracer and the graphical profiler.

### YAP profilers

Logtalk supports the [YAP](http://www.cos.ufrj.br/~vitor/Yap/) tick and count profilers. See the `profiler` tool in the current Logtalk distribution for details.

### SICStus Prolog profilers

Logtalk supports the [SICStus Prolog 4](http://www.sics.se/isl/sicstus.html) profiler. See the `profiler` tool in the current Logtalk distribution for details.

### PDT

[PDT](https://sewiki.iai.uni-bonn.de/research/pdt/docs/start) is an open source Prolog IDE provided as a plug-in for the Eclipse IDE. PDT is being extended with Logtalk support.

PDT currently requires a recent version of SWI-Prolog. It's possible to start up Logtalk automatically by configuring PDT runtime preferences. The configuration depends on the operating-system. After installing Logtalk and setting the `LOGTALKHOME` and `LOGTALKUSER` environment variables, open Eclipse preferences, select PDT runtime preferences, and enter the following configuration data for the SWI-Prolog executable and for the extra environment variables (change the paths to match your SWI-Prolog and Logtalk installations and your home directory):

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

After saving the `Info.plist` file, close TextMate if open and re-open it. Then try to a QuickLook a Logtalk source file. You should get a preview window with nice syntax highlighting for your code. If not, move the TextMate application to a different folder (e.g. you Desktop) and then back to its original location. This is usually enough to get the Finder to notice and register the Quick Look changes in the application bundle.
