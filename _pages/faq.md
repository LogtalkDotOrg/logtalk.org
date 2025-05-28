::: {.header}
[Home](logtalk.html) \> [Documentation](documentation.html) \> FAQ
:::

::: {.title}
Frequently Asked Questions
:::

 

General
:   [Why are all versions of Logtalk numbered 2.x or 3.x?](#general-1)
:   [Why do I need a Prolog compiler to use Logtalk?](#general-2)
:   [Is the Logtalk implementation based on Prolog modules?](#general-3)
:   [Does the Logtalk implementation use term-expansion?](#general-4)

<!-- -->

Compatibility
:   [Can I use constraint-based packages with
    Logtalk?](#compatibility-1)
:   [Can I use Logtalk objects and Prolog modules at the same
    time?](#compatibility-2)

<!-- -->

Installation
:   [The integration scripts are not working!](#installation-1)
:   [I get some errors while starting up Logtalk after upgrading to the
    latest version!](#installation-2)

<!-- -->

Portability
:   [Are my Logtalk applications portable across Prolog
    compilers?](#portability-1)
:   [Are my Logtalk applications portable across operating
    systems?](#portability-2)

<!-- -->

Programming
:   [Should I use prototypes or classes in my
    application?](#programming-1)
:   [Can I use both classes and prototypes in the same
    application?](#programming-2)
:   [Can I mix classes and prototypes in the same
    hierarchy?](#programming-3)
:   [Can I use a protocol or a category with both prototypes and
    classes?](#programming-4)
:   [What support is provided in Logtalk for defining and using
    components?](#programming-5)
:   [What support is provided in Logtalk for reflective
    programming?](#programming-6)

<!-- -->

Troubleshooting
:   [Using compiler options on calls to the Logtalk compiling and
    loading predicates do not work!](#troubleshooting-1)
:   [Gecko-based browsers (e.g. Firefox) show non-rendered HTML entities
    when browsing XML documenting files!](#troubleshooting-2)
:   [Compiling a source file results in errors or warnings but the
    Logtalk compiler reports a successful compilation with zero errors
    and zero warnings!](#troubleshooting-3)

<!-- -->

Usability
:   [Is there a shortcut for compiling and loading source
    files?](#usability-1)
:   [Is there an equivalent directive to the `ensure_loaded/1` Prolog
    directive?](#usability-2)
:   [Are there shortcuts for the *make* functionality?](#usability-3)

<!-- -->

Deployment
:   [Can I create standalone applications with Logtalk?](#deployment-1)

<!-- -->

Performance
:   [Is Logtalk implemented as a meta-interpreter?](#performance-1)
:   [What kind of code Logtalk generates when compiling objects? Dynamic
    code? Static code?](#performance-2)
:   [How about message-sending performance? Does Logtalk use static
    binding or dynamic binding?](#performance-3)
:   [Which Prolog-dependent factors are most crucial for good Logtalk
    performance?](#performance-4)
:   [How does Logtalk performance compares with plain Prolog and with
    Prolog modules?](#performance-5)

<!-- -->

Licensing
:   [Can Logtalk be used in commercial applications?](#licensing-2)

<!-- -->

Consulting and support
:   [Are there other consulting, training and supporting services
    besides the ones described on this web site?](#support-1)

 

::: {.subtopictitle}
General
:::

> []{#general-1}*Why are all versions of Logtalk numbered 2.x or 3.x?*
>
> The numbers \"2\" and \"3\" in the Logtalk version string refers to,
> respectively, the second and the third generations of the Logtalk
> language. Development of Logtalk 2 started on January 1998, with the
> first alpha release for registered users on July and the first public
> beta on October. The first stable version of Logtalk 2 was released on
> February 9, 1999. Development of Logtalk 3 started on April 2012, with
> the first public alpha released on August 21, 2012. The first stable
> version of Logtalk 3 was released on January 7, 2015.

> []{#general-2}*Why do I need a Prolog compiler to use Logtalk?*
>
> Currently, the Logtalk language is implemented as a Prolog extension
> instead of as a standalone compiler. Compilation of Logtalk source
> files is performed in two steps. First, the Logtalk compiler converts
> a source file to a Prolog file. Second, the chosen Prolog compiler is
> called by Logtalk to compile the intermediate Prolog file generated on
> the first step. The implementation of Logtalk as a Prolog extension
> allows users to use Logtalk together with features only available on
> specific Prolog compilers.

> []{#general-3}*Is the Logtalk implementation based on Prolog modules?*
>
> No. Logtalk is (currently) implemented is plain Prolog code. Only a
> few Prolog compilers include a module system, with several
> compatibility problems between them. Moreover, the current ISO Prolog
> standard for modules is next to worthless and is ignored by most of
> the Prolog community. Nevertheless, the Logtalk compiler is able to
> compile simple modules (using a common subset of module directives) as
> objects for backward-compatibility with existing code (see the [Prolog
> integration and migration guide](handbook/userman/migration.html) for
> details).

> []{#general-4}*Does the Logtalk implementation use term-expansion?*
>
> No. Term-expansion mechanisms are not standard and are not available
> in all supported Prolog compilers.

::: {.subtopictitle}
Compatibility
:::

> []{#compatibility-1}*Can I use constraint-based packages with
> Logtalk?*
>
> Usually, yes. Some constraint-based packages may define operators
> which clash with the ones defined by Logtalk. In these cases,
> compatibility with Logtalk depends on the constraint-based packages
> providing an alternative for accessing the functionality provided by
> those operators. When the constraint solver is encapsulated using a
> Prolog module, a possible workaround is to use explicit module
> qualification, encapsulating the call using the `{}/1` Logtalk control
> construct (thus bypassing the Logtalk compiler).

> []{#compatibility-2}*Can I use Logtalk objects and Prolog modules at
> the same time?*
>
> Yes. In order to call a module predicate from within an object (or
> category) you may use a `use_module/2` directive or use explicit
> module qualification (possibly wrapping the call using the Logtalk
> control construct `{}/1` that allows bypassing of the Logtalk compiler
> when compiling a predicate call). Logtalk also allows modules to be
> compiled as objects (see the [Prolog integration and migration
> guide](handbook/userman/migration.html) for details).

::: {.subtopictitle}
Installation
:::

> []{#installation-1}*The integration scripts/shortcuts are not
> working!*
>
> Check that the `LOGTALKHOME` and `LOGTALKUSER` environment variables
> are defined, that the Logtalk user folder is available on the location
> pointed by `LOGTALKUSER` (you can create this folder by running the
> shell script `cplgtdirs`), and that the Prolog compilers that you want
> to use are supported and available from the system path. If the
> problem persists, run the shell script that creates the integration
> script or shortcut manually and check for any error message or
> additional instructions. For some Prolog compilers such as XSB and
> Ciao, the first call of the integration script or shortcut must be
> made by an administrator user. If you are using Windows, make sure
> that any anti-virus or other security software that you might have
> installed is not silently blocking some of the installer tasks.

> []{#installation-2}*I get some errors while starting up Logtalk after
> upgrading to the latest version!*
>
> Changes in the Logtalk compiler between releases may render Prolog
> config files from older versions incompatible with new ones. You may
> need to update your local Logtalk user files by running e.g. the
> `logtalk_user_setup` shell script. Check the `UPGRADING.md` file on
> the root of the Logtalk installation directory and the release notes
> for any incompatible changes to the config files.

::: {.subtopictitle}
Portability
:::

> []{#portability-1}*Are my Logtalk applications portable across Prolog
> compilers?*
>
> Yes, as long you don\'t use built-in predicates or special features
> only available on some Prolog compilers. There is a compiler flag
> (`portability`) that you can set to instruct Logtalk to print a
> warning for each call in your code of non-ISO Prolog standard built-in
> predicates. In addition, it is advisable that you constrain, if
> possible, the use of platform or compiler dependent code to a small
> number of objects with clearly defined protocols. You may also use
> Logtalk support for conditional compilation to compile different
> entity or predicate definitions depending on the backend Prolog
> compiler being used.

> []{#portability-2}*Are my Logtalk applications portable across
> operating systems?*
>
> Yes. However, you may need to change the end-of-lines characters of
> your source files to match the ones on the target operating system and
> the expectations of your Prolog compiler. Some Prolog compilers
> silently fail to compile source files with the wrong end-of-lines
> characters.

::: {.subtopictitle}
Programming
:::

> []{#programming-1}*Should I use prototypes or classes in my
> application?*
>
> Prototypes and classes provide different forms of code reuse. A
> prototype encapsulates code that can be used by itself and by its
> descendent prototypes. A class encapsulates code to be used by its
> descendent instances. Prototypes provide the best replacement to the
> use of modules as encapsulation units, avoiding the need to
> instantiate a class in order to access its code.

> []{#programming-2}*Can I use both classes and prototypes in the same
> application?*
>
> Yes. In addition, you may freely exchange messages between prototypes,
> classes, and instances.

> []{#programming-3}*Can I mix classes and prototypes in the same
> hierarchy?*
>
> No. However, you may define as many hierarchies of prototypes and
> classes as needed by your application.

> []{#programming-4}*Can I use a protocol or a category with both
> prototypes and classes?*
>
> Yes. A protocol may be implemented by both prototypes and classes in
> the same application. Likewise, a category may be imported by both
> prototypes and classes in the same application.

> []{#programming-5}*What support is provided in Logtalk for defining
> and using components?*
>
> Logtalk supports component-based programming (since its inception on
> January, 1998), by using *categories* (which are first-class entities
> like objects and protocols). Logtalk categories can be used with both
> classes and prototypes and are inspired on the Smalltalk-80
> (documentation-only) concept of method categories and on Objective-C
> categories, hence the name. For more information, please consult the
> [documentation](documentation.html) and the examples provided with the
> system.

> []{#programming-6}*What support is provided in Logtalk for reflective
> programming?*
>
> Logtalk supports meta-classes, behavioral reflection through the use
> of event-driven programming, and structural reflection through the use
> of a set of built-in predicates and built-in methods which allow us to
> query the system about existing entities, entity relations, and entity
> predicates.

::: {.subtopictitle}
Troubleshooting
:::

> []{#troubleshooting-1}*Using compiler options on calls to the Logtalk
> compiling and loading predicates do not work!*
>
> Using compiler options on calls to the Logtalk `logtalk_compile/2` and
> `logtalk_load/2` built-in predicates only apply the file being
> compiled. If the first argument is a *loader* file, the compiler
> options will only be used in the compilation of the loader file
> itself, not in the compilation of the files loaded by the loader file.
> The solution is to edit the loader file and add the compiler options
> to the calls that compile/load the individual files.

> []{#troubleshooting-2}*Gecko-based browsers (e.g. Firefox) show
> non-rendered HTML entities when browsing XML documenting files!*
>
> Using Gecko-based browsers (e.g. Firefox) show non-rendered HTML
> entities (e.g. `&ndash;`) when browsing XML documenting files after
> running the `lgt2xml` shell script in the directory containing the XML
> documenting files. This is a consequence of the lack of support for
> the `disable-output-escaping` attribute in the browser XSLT processor.
> The workaround is to use other browser (e.g. Safari or Opera) or to
> use instead the `lgt2html` shell script in the directory containing
> the XML documenting files to convert them to (X)HTML files for
> browsing.

> []{#troubleshooting-3}*Compiling a source file results in errors or
> warnings but the Logtalk compiler reports a successful compilation
> with zero errors and zero warnings!*
>
> This may happen when your Prolog compiler implementation of the ISO
> Prolog standard `write_canonical/2` built-in predicate is buggy and
> writes terms that cannot be read back when consulting the intermediate
> Prolog files generated by the Logtalk compiler. Often, syntax errors
> found when consulting result in error messages but not in exceptions
> as the Prolog compiler tries to continue the compilation despite the
> problems found. As the Logtalk compiler relies on the exception
> mechanisms to catch compilation problems, it may report zero errors
> and zero warnings despite the error messages. Send a bug report to the
> Prolog compiler developers asking them to fix the `write_canonical/2`
> buggy implementation.

::: {.subtopictitle}
Usability
:::

> []{#usability-1}*Is there a shortcut for compiling and loading source
> files?*
>
> Yes. With most backend Prolog compilers, you can use `{File}` as a
> shortcut for `logtalk_load(File)`. For compiling and loading multiple
> files simply use `{File1, File2, ...}`.

> []{#usability-2}*Is there an equivalent directive to the
> `ensure_loaded/1` Prolog directive?*
>
> You can use the goal `logtalk_load(File, [reload(skip)])` to ensure
> that `File` is only loaded once.

> []{#usability-3}*Are there shortcuts for the *make* functionality?*
>
> Yes. With most backend Prolog compilers, you can use `{*}` as a
> shortcut for `logtalk_make(all)` to reload all files modified since
> last compiled and loaded, `{!}` as a shortcut for
> `logtalk_make(clean)` to delete all intermediate Prolog files
> generated by the compilation of Logtalk source files, `{?}` as a
> shortcut for `logtalk_make(missing)` to list missing entities and
> predicates, and `{@}` as a shortcut for `logtalk_make(circular)` to
> list circular references.

::: {.subtopictitle}
Deployment
:::

> []{#deployment-1}*Can I create standalone applications with Logtalk?*
>
> It depends on the Prolog compiler that you use to run Logtalk.
> Assuming that your Prolog compiler supports the creation of standalone
> executables, your application must include the config file for your
> compiler and the Logtalk compiler and runtime.
>
> For instructions on how to embed Logtalk and Logtalk applications see
> the [Logtalk wiki section on
> embedding](embedding.html).

::: {.subtopictitle}
Performance
:::

> []{#performance-1}*Is Logtalk implemented as a meta-interpreter?*
>
> No. Objects and their encapsulated predicates are compiled, not
> meta-interpreted. In particular, inheritance relations are
> pre-compiled for improved performance. Moreover, no meta-interpreter
> is used even for objects compiled in debug mode.

> []{#performance-2}*What kind of code Logtalk generates when compiling
> objects? Dynamic code? Static code?*
>
> Static objects are compiled to static code. Static objects containing
> dynamic predicates are also compiled to static code, except, of
> course, for the dynamic predicates themselves. Dynamic objects are
> necessarily compiled to dynamic code. As in Prolog programming, for
> best performance, dynamic object predicates and dynamic objects should
> only be used when truly needed.

> []{#performance-3}*How about message-sending performance? Does Logtalk
> use static binding or dynamic binding?*
>
> Logtalk supports both static binding and dynamic binding. When static
> binding is not possible, Logtalk uses dynamic binding coupled with a
> caching mechanism that avoids repeated lookups of predicate
> declarations and predicate definitions. This is a solution common to
> other programming languages supporting dynamic binding. Message
> lookups are automatically cached the first time a message is sent.
> Cache entries are automatically removed when loading entities or using
> Logtalk dynamic features that invalidate the cached lookups. Whenever
> static binding is used, message sending performance is essentially the
> same as a predicate call in plain Prolog. Performance of dynamic
> binding when lookups are cached is close to the performance that would
> be achieved with static binding. See the [Logtalk wiki section on
> performance](performance.html)
> for more details.

> []{#performance-4}*Which Prolog-dependent factors are most crucial for
> good Logtalk performance?*
>
> Logtalk compiles objects assuming first-argument indexing for static
> code. First-argument indexing of dynamic code, when available, helps
> improving performance due to the automatic caching of method lookups
> and the necessary use of book-keeping tables by the runtime engine
> (this is specially important when using event-driven programming).
> Dynamic objects and static objects containing dynamic predicates also
> benefit from first-argument indexing of dynamic predicates. The
> availability of multi-argument indexing, notably for dynamic
> predicates, also benefits dynamic binding performance.

> []{#performance-5}*How does Logtalk performance compares with plain
> Prolog and with Prolog modules?*
>
> Plain Prolog, Prolog modules, and Logtalk objects provide different
> trade-offs between performance and features. In general, for a given
> predicate definition, the best performance will be attained using
> plain Prolog, second will be Prolog modules (assuming no explicitly
> qualified calls are used), and finally Logtalk objects. Whenever
> static binding is used, the performance of Logtalk is equal or close
> to that of plain Prolog (depending on the Prolog virtual machine
> implementation and compiler optimizations). You can find
> [here](performance.html) some simple benchmark tests using some
> popular Prolog compilers.

::: {.subtopictitle}
Licensing
:::

> []{#licensing-2}*Can Logtalk be used in commercial applications?*
>
> Yes. Logtalk follows the [Apache Licence
> 2.0](https://github.com/LogtalkDotOrg/logtalk3/blob/master/LICENSE.txt).

::: {.subtopictitle}
Consulting and support
:::

> []{#support-1}*Are there consulting, training and supporting services
> besides the ones described on this web site?*
>
> Yes. Please visit [logtalk.pt](http://logtalk.pt) for commercial
> consulting, developing, training, and other supporting services.

 

::: {.navigation}
[News](news.html) • [Features](features.html) • [Compatibility](compatibility.html) • [Documentation](documentation.html) • [Download](download.html) • [Developers](https://github.com/LogtalkDotOrg/logtalk3/) • [Support](support.html) • [Chat](https://gitter.im/LogtalkDotOrg/logtalk3) • [Forums](http://forums.logtalk.org/) • [Links](links.html) • [Blog](http://blog.logtalk.org/) • [Twitter](http://twitter.com/LogtalkDotOrg)
:::

::: {.footer}
[ [XHTML](http://validator.w3.org/check/referer) +
[CSS](http://jigsaw.w3.org/css-validator/check/referer)\
<webmaster@logtalk.org> ]{.left}

[ September 14, 2018\
© Paulo Moura, 1998-2018 ]{.right}

[web hosting supporting
donations](http://www.dreamhost.com/donate.cgi?id=7489)
:::
