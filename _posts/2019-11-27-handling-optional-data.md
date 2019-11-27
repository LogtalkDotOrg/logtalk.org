---
layout: article
title: Handling optional data
tags:
  - best practices
show_edit_on_github: false
aside: false
---

We often need to represent structured data where some of the data is
optional. As an example, consider books that may be sold with extras:

```logtalk
% book(Name, Author, Year)
book('The Philosopher''s Stone', 'J. K. Rowling', 1997).
book('The Chamber of Secrets',   'J. K. Rowling', 1998).
book('The Prisoner of Azkaban',  'J. K. Rowling', 1999).
book('The Goblet of Fire',       'J. K. Rowling', 2000).
book('The Order of the Phoenix', 'J. K. Rowling', 2003).
book('The Half-Blood Prince',    'J. K. Rowling', 2005).
book('The Deathly Hallows',      'J. K. Rowling', 2007).

% extra(Title, Extra)
extra('The Philosopher''s Stone', quidditch_set).
extra('The Chamber of Secrets',   map).
extra('The Half-Blood Prince',    audio_cd).
extra('The Deathly Hallows',      horcrux_set).
```

To make the example more interesting, assume that some of the extras are
heavy enough for their weight to be declared (e.g. for calculating postage
fees):

```logtalk
% weight(Extra, Weight)
weight(quidditch_set, 278).
weight(horcrux_set,   123).
```

I.e. we have books that may have extras that, in turn, may have a declared
weight. A traditional solution for representing optional data is to use some
concept of a [*null value*](https://en.wikipedia.org/w/index.php?title=Null_pointer).
The trouble of this solution is that it forces us to test for the
presence of a null value every time we process an optional item. In the
particular case of Logtalk or Prolog, an alternative solution is to rely
on the [closed-world assumption](https://logtalk.org/manuals/glossary.html#term-closed-world-assumption)
(e.g. assuming that *The Goblet of Fire* isn't bundled with an extra as
there's no corresponding `extra/2` fact for it). But that only saves us from
deciding how to represent a null value. For example, if we wanted to print a
full description of a book, we would print the title, author, publishing year,
and then if there's an extra we would print its name and then if the extra
have a declared weight we would print it as well:

```logtalk
print_book(Title) :-
    book(Title, Author, Year),
    write(Title), write(' by '), write(Author), write(' on '), write(Year), nl,
    (   extra(Title, Extra) ->
        write('  with free '), write(Extra),
        (   weight(Extra, Weight) ->
            write(' ('), write(Weight), write(' gr)')
        ;   true
        ),
        nl
    ;   true.
    ).
```

This is cumbersome code. It would be slightly better if `format/2-3` was
actually a standard predicate. But the point is that testing for each optional
item scales poorly as soon as we have more than a couple of optional items or
when optional items can have themselves optional items. These nested
conditionals would also have to be used in multiple places (e.g. when computing
a postage fee that depends on the optional extra and on the optional declared
weight of the extra).

When we discussed [handling of missing data](https://logtalk.org/2019/11/21/handling-missing-data.html),
we highlighted the importance of minimizing the coupling between *data acquisition* and *data
processing*. Here, we also want to represent optional data in a way that
postpones to data processing deciding how to deal with it. Logtalk
provides a [`optionals`](https://logtalk.org/library/library_index.html#optionals)
library that allows convenient representation of the optional data by
providing predicates for constructing and handling *optional terms*, which
are opaque terms that either hold a value or the information that a value
is absent.

Assume that our data acquisition step translates to a `book/4` predicate that
provides a unified view of book data. Instead of using a special value to
represent the absence of a book extra, we use an optional term to represent the
possible existence of an extra. As some extras have a declared weight, we use a
second optional term for the weight:

```logtalk
book(Title, Author, Year, OptionalExtra) :-
    book(Title, Author, Year),
    optional::from_goal(extra(Title, Extra), Extra-OptionalWeight, OptionalExtra),
    optional::from_goal((extra(Title, Extra), weight(Extra, Weight)), Weight, OptionalWeight).
```

The [`optional::from_goal(Goal, Value, Optional)`](https://logtalk.org/library/optional_0.html#from-goal-3)
predicate takes a goal that when succesful binds the value to be hold by the
optional term. When the goal fails, the predicate returns an empty optional
term. How do we process optional terms? The `print_book/1` predicate above
can be rewritten as:

```logtalk
print_book(Title) :-
    book(Title, Author, Year, Extra),
    write(Title), write(' by '), write(Author), write(' on '), write(Year), nl,
    optional(Extra)::if_present(print_book_extra).

print_book_extra(Extra-Weight) :-
    write('  with free '), write(Extra),
    optional(Weight)::if_present([Grams]>>(write(' ('), write(Weight), write(' gr)'))),
    nl.
```

The [`optional(Optional)::if_present(Closure)`](https://logtalk.org/library/optional_1.html#if-present-1)
predicate applies a closure to the value hold by the optional term. When the
optional term is empty, the predicate simply succeeds. The `print_book_extra/1`
predicate prints the extra weight, when present, in grams. Le's assume that
we wanted instead to express the weight in kilograms. That requires mapping
the optional weight from grams to kilograms:

```logtalk
print_book_extra(Extra-WeightGrams) :-
    write('  with free '), write(Extra),
    optional(WeightGrams)::map([Grams,Kilos]>>(Kilos is Grams / 1000), WeightKilos),
    optional(WeightKilos)::if_present([Kilograms]>>(write(' at '), write(Kilograms), write(' kg'))),
    nl.
```

The [`optional(Optional)::map(Closure, NewOptional)`](https://logtalk.org/library/optional_1.html#map-2)
predicate applies a closure to the value hold by the optional term and
the new value, returning a new optional holding the new value. When the
optional term is empty, it simply returns it.

The [`optionals`](https://logtalk.org/library/library_index.html#optionals)
library provides other useful predicates for constructing and handling
optional terms. For example, assume that we want a list of titles of the
books that are bundled with extras:

```logtalk
books_with_extras(Titles) :-
    findall(
        Title,
        (   book(Title, _Author, _Year, Extra),
            optional(Extra)::is_present
        ),
        Titles
    ).
```

The [`optional(Optional)::is_present`](https://logtalk.org/library/optional_1.html#is-present-0)
predicate succeeds or fails depending on the optional term holding a
value. Several of the library predicates allow us to either get the value
hold by an optional term or act in its absence. For example, assume
that the post office requires a default weight of 20 grams to process
postage fees of books with extras:

```logtalk
    ..., optional(Weight)::or_else(Grams, 20), ...
```
The [`optional(Optional)::or_else(Value, Default)`](https://logtalk.org/library/optional_1.html#or-else-2)
predicate returns in its first argument the value hold by the optional
term or the given default value if the optional term is empty. As a last
example, assume that we want to print a listing of all the books with
extras reusing the `print_book_extra/1` predicate we defined earlier:

```logtalk
print_books_with_extras :-
    book(Title, Author, Year, Extra),
    optional(Extra)::or_else_fail(Data),
    write(Title), write(' by '), write(Author), write(' on '), write(Year), nl,
    print_book_extra(Data),
    fail.
print_books_with_extras.
```

In this case, we used the [`optional(Optional)::or_else_fail(Value)`](https://logtalk.org/library/optional_1.html#or-else-fail-1)
predicate to either get the value hold by an optional term or fail,
backtracking into the next book. Consult the library documentation
for other available predicates.

Our final notes are about performance. The use of the
[`optional/1`](https://logtalk.org/library/optional_1.html)
parametric object enables [static binding](https://logtalk.org/manuals/glossary.html#term-static-binding)
to be used for all calls to the predicates that operate on optional terms for efficient processing.
Internally, optional terms use a simple representation for
wrapped values and empty optionals thus minimizing memory overhead.

### Resources

The Logtalk distribution includes the full source code of the
[`books`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/books)
example used as basis for this blog post.
