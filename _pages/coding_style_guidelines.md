---
layout: article
permalink: coding_style_guidelines.html
title: Coding Style Guidelines
aside:
  toc: true
---

In general, Prolog coding style guidelines also apply to Logtalk programming. Guidelines, including this one, should be taken as recommendation rather than dogma. Strict use of the guidelines here presented is only expected when contributing to the Logtalk distribution. When adapting this or other guidelines, the golden rule is consistency and consensus within your development team.

Organizing your source files
----------------------------

Store your files in a directory with a simple but descriptive name. Avoid using a name already in use in the current Logtalk distribution. Besides your source files, the directory often contains utility and documentation files such as:

* A loader file for your source files. Usually named `loader.lgt`, this file should load both your source files and any other files (e.g. library files) needed for compiling and running your code. Loader files may also be used to set appropriated flags for compiling and loading your source files. You may also want to have e.g. a `loader_debug.lgt` file if there's a non-trivial debugging setup for developing your code.

* An informative `NOTES.md` or `NOTES.txt` file with a description of your code, authorship, copyright, and licensing information.

* A `SCRIPT.txt` file containing instructions on how to load your source files and sample queries.

* A loader file for your tests (which also loads your source files), usually named `tester.lgt` (this is the name expected by the testing automation script), side-by-side with ​the `loader.lgt` file (so that the user can run your code tests simply by replacing `loader` by `tester` in the `logtalk_load/1` goal that loads your code).

* A file contain your unit tests, usually named `tests.lgt`. If there's a single tests file, keep it in the same directory as the ​`loader.lgt` and `tester.lgt`​ files. If there are multiple test files, use a `tests` or `test_files` sub-directory.

* A _doclet_ file for generating documentation and diagrams for your source code, usually named `doclet.lgt` (this is the name expected by the doclet automation script).

If you are using a version control system, the [coding](https://github.com/LogtalkDotOrg/logtalk3/tree/master/coding) directory contains _ignore files_ for several systems.

Source file names
-----------------

Logtalk source files use by default the `.lgt` file name extension. You can also use in alternative the `.logtalk` extension. When a source file contains a single entity, use the entity name for the source file name. For parametric objects and parametric categories, append the number of parameters to the file name. For source files containing multiple entities, use a descriptive name. In this case, the name is often the same as the name of the directory holding your files.

Source file text encoding
-------------------------

Use preferably US-ASCII or a Unicode encoding such as UTF-8. Avoid ISO-Latin-X text encodings unless that's required by limitations on the backend Prolog compiler or client requirements. Ensure that any used text editor can correctly handle the chosen encoding.

Source code layout and indentation
----------------------------------

Indent your source file using tabs, not spaces. Never mix tabs and spaces for indentation. But do use spaces for alignment that is not related to indenting. One tab is one level of indentation and is **independent** of each team member preferred setting, contributing to **accessibility**. A common setting is a tab width equivalent to four spaces. **Check that when changing the tab width that your code and comments remain perfectly indented**. Use one tab for indenting the code encapsulated inside an entity. Indent the body of predicate clauses using one tab.

Clauses for the same predicate should be separated by at most one blank line. Closely related predicates (e.g. a predicate followed by its auxiliary predicates) should be separated by one or two blank lines. Clauses of other predicates can be separated by two or three blank lines, depending on code complexity.

Directives layout
-----------------

The recommended layout for `initialization /1` directives is:

```logtalk
:- initialization((
    goal1,
    goal2,
    ...
)).
```

A single tab/level of indentation is used for the directive arguments. The closing parentheses are aligned with the directive operator so that the alignment is preserved no matter the personal choice for the tab setting. Similar for other directives. For example:

```logtalk
:- info([
    version is 1.1,
    author is 'John Doe',
    date is 2016/11/21,
    comment is 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
]).

:- uses(list, [
    append/3, member/2, select/3
]).
```

Comments
--------

General comments on entities and predicates can often be moved to entity `info/1` and predicate `info/2` directives. The documenting tool can then be used to extract, format, and publish that information. Outside these directives, use code comments for information that is not obvious from predicate names and variable names. Write "inline" comments in a new line instead of in the same line after the code. For example:

```logtalk
...,
goal1,
% comment about the previous goal or about the next goal
goal2,
% ...
....
```

This helps avoiding long lines, keeps the comments aligned with the code, and allows breaking long clauses into sections.

Clause heads
------------

Long clause heads are sometimes unavoidable. For readability and independence of the personal choice for tab width, write: 

```logtalk
predicate_name(
    first_argument, second_argument, ...,
    n_argument, ...
) :-
    ...
```

Trying to align the arguments with the opening parenthesis would make the alignment break under different tab widths or even worse could result in a mix of tabs and spaces for indentation.

Goals in clause bodies
----------------------

As a general rule, write one goal per line. Exceptions are green cuts and goals like `nl` after a write term goal. In this case, write the two goals in the same line. Red cuts should always be written in a separate line.

Complex goals can be more readable, however, using several lines. For example:

```logtalk
...,
setof(
    Template,
    (   current_predicate(Functor/Arity),
        functor(Template, Functor, Arity)
    ),
    Templates
),
...
```

Note the parenthesis alignment.

Meta-arguments
--------------

Goal arguments in meta-predicates calls (e.g. `findall/3`) should be simple. Ideally, a single predicate call. Complex meta-arguments are hard to read, debug, and, depending on the backend Prolog compiler, may result in poor performance. In some cases, a lambda expression can be used to avoid adding an auxiliary predicate just for the meta-call.

Disjunctions
------------

Disjunctions should always be wrapped between parenthesis and the `;` operator should be the first term in the line. For example:

```logtalk
...
(   alternative1
;   alternative2
;   ...
),
...
```

When the disjunction is the sole goal in a clause body, use instead separate clauses. For example, instead of:

```logtalk
head :-
    (   alternative1
    ;   alternative2
    ).
```

write instead:

```logtalk
head :-
    alternative1.
head :-
    alternative2.
```

One exception to this guideline is when the head of the clause performs costly access to a sub-term in complex compound argument.

If-then-else constructs
-----------------------

Always use parenthesis around if-then-else constructs and always include the "else" part. I.e. write if necessary `(If -> Then; fail)` instead of `(If -> Then)`. An actual example of the recommended layout:

```logtalk
is_prime(N, Sqrt, Prime) :-
    (   N > Sqrt ->
        true
    ;   Prime mod N > 0,
        N2 is N + 2,
        is_prime(N2, Sqrt, Prime)
    ).
```

Use a tab between the opening parenthesis and the first goal. Also use a tab between the `;` and the goal that follows. Align vertically the opening parenthesis, the `;`, and the closing parenthesis. A common variant is to write:

```logtalk
is_prime(N, Sqrt, Prime) :-
    (   N > Sqrt
    ->  true
    ;   Prime mod N > 0,
        N2 is N + 2,
        is_prime(N2, Sqrt, Prime)
    ).
```

Choose a variant and use it consistently.


Failure-driven loops
--------------------

Indent with one tab the goals between the generator goal and the goal that forces backtracking. For example:

```logtalk
write_person_database :-
    person(Name, Age),
        write('Name: '), write(Name), nl,
        write('Age: '), write(Age), nl, nl,
    fail.
write_person_database.
```

In cases where a failure-driven loop can mask unexpected failures, consider using in alternative the `forall/2` meta-predicate.

Predicate arguments
-------------------

Use a single space after commas that separate predicate arguments to improve readability.

Operators
---------

As a general rule, use spaces around binary operators. E.g. write `Total is Sum * N - OverHead`, not `Total is Sum*N-OverHead`.

List elements
-------------

Use a single space after commas that separate elements. Also use a single space after the `|` separating the enumerated elements from the list with the remaining elements. I.e. write `[First, Second| Rest]`, not `[First,Second|Rest]`.

Clause rules and directives
---------------------------

Use a single space before the `:-` operator in clause rules. Use a single space after the `:-` operator in directives.

Entity names
------------

For object, protocol, and category names, observe the same guidelines as for predicate names.

Predicate names
---------------

Use descriptive predicate names using underscores if necessary to link words. Do not use CamelCase notation for predicate names (e.g. write `number_of_sides`, not `numberOfSides`). Avoid word abbreviations. But if you abbreviate a word, do so consistently. Also avoid names with digits in the middle as this may hurt readability.

For dynamic predicates, Logtalk uses a convention of ending its names with an underscore (e.g. `random_seed_`) although this style is sometimes also used for auxiliary predicate names.

For public predicates, when defining an interface, always consider reusing names. This makes APIs easier to understand and use. For example, the predicate `member/2` is used with both lists and sets. The predicate `size/2` is used with both dictionaries and heaps. Most developer tools that require processing files, directories, and libraries share a common interface.

Variable names
--------------

Use descriptive variable names in CamelCase notation (e.g. write `SourceFile`, not `Source_file`). Again, avoid word abbreviations. But if you do abbreviate words, be consistent. Also avoid names with digits in the middle as this may hurt readability.

In the case of singleton variables, use either the anonymous variable, `_`, or a variable name starting with an underscore followed with an uppercase letter (e.g. `_Width`). Note that the interpretation of variables that start with an underscore as either singleton variables or anonymous variables depends on the used back-end compiler (see the Logtalk compiler flag `underscore_variables` for more information).

Sequences
---------

Arguments that represent a sequence of *states*, e.g. successive values of an accumulator, should be represented using variables named `S0`, `S1`, ..., `S`, with `S` replaced by an adequate argument name. For example:

```logtalk
sum_list(List, Sum) :-
    sum_list(List, 0, Sum).

sum_list([], Sum, Sum).
sum_list([Value| Values], Sum0, Sum) :-
    Sum1 is Sum0 + Value,
    sum_list(Values, Sum1, Sum).
```

Top-level interpreter shortcuts
-------------------------------

Logtalk (and Prolog) define top-level interpreter shortcuts for loading source files and for `make` tasks. These shortcuts are **not** part of the language and should only be used at the top-level interpreter and never in source files.
