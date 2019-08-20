---
layout: article
title: "Failure-driven loops: when and how"
tags:
  - loops
  - best practices
show_edit_on_github: false
aside: false
---

**Failure is a big part of logic programming success!** (always wanted to write this :-)

Predicates are often required to perform repetitive operations. For example, assume a table of pet names:

```logtalk
pet(garfield).
pet(odie).
```

To print all the pet names, one per line, we may define the following predicate:

```logtalk
write_pet_names :-
    pet(Name),
    write(Name), nl,
    fail.
write_pet_names.
```

This predicate definition is an example of a *traditional failure-driven loop*. After finding a solution for the `pet/1` predicate, we print the pet name and then call `fail/0`, forcing backtracking. As `write/1` and `nl/0` are deterministic predicates, we backtrack into the `pet/1` call, retrieving the next pet name (if any). After exhausting all solutions for the `pet(Name)` goal, the inference engine backtracks into the second clause of the `write_pet_names/0` predicate, which trivially succeeds:

```text
| ?- write_pet_names.

garfield
odie
yes
```

Failure-driven loops can be applied whenever we want to prove something for each solution of a goal but without requiring saving the set of generated solutions for later processing.

But is the traditional failure-driven loop a *safe programming idiom*? Let's make a small change to the predicate: before printing a pet name, we convert it to title case. In a hurry and half-a-sleep, we write a badly broken auxiliary predicate:

```logtalk
title_case(Name, TitleCase) :-
    atom_codes(Name, [LowerCase| Codes]),
    0'a =< LowerCase, LowerCase =< 0'z,
    UpperCase is 0'A + LowerCase - 0'a,
    atom_codes(TitleCase, [UpperCase| Codes]).
```

We do a quick test and all seems good:

```text
| ?- title_case(garfield, TC).

TC = 'Garfield'
yes
```

The updated `write_pet_names/0` predicate becomes:

```logtalk
write_pet_names :-
    pet(Name),
    title_case(Name, TitleCase),
    write(TitleCase), nl,
    fail.
write_pet_names.
```

We move happily to the next programming task, oblivious that later a co-worker updated the `pet/1` table with the name of its new cat, Kitty:

```logtalk
pet(garfield).
pet('Kitty').
pet(odie).
```

We now get:

```text
| ?- write_pet_names.

Garfield
Odie
yes
```

Kitty have gone missing and no one notices! The upstream bug is, of course, in our badly broken auxiliary predicate, `title_case/2`,  which fails (among other cases) when the name is already in title case. But because we are **using a traditional failure-driven loop, the unexpected failure is masked away**: the `title_case('Kitty', TitleCase)` goal fails and the code simply backtracks into the next solution for the `pet/1` predicate. Thus, **traditional failure-driven loops should be used with cautious and only when unexpected failures cannot occur and introduce bugs in the expected results**. Note that our first definition of the `write_pet_names/0` predicates is safe: `pet/1` is a table of facts (which, if not defined, and assuming a static predicate, would result in a predicate existence error) and the `write/1` and `nl/0` predicates either succeed or throw an error (likely, stream related). Nothing in the `write_pet_names/0` predicate catches erros and thus we will notice if something goes wrong.

Is there a safer way of implementing a failure-driven loop? The de facto standard `forall/2` predicate provides a partial answer. This meta-predicate implements a *generate-and-test* loop that subsumes failure-driven loops and can be defined as:

```logtalk
forall(Generate, Test) :-
    \+ (Generate, \+ Test).
```

We can use it to reimplement the `write_pet_names/0` predicate:

```logtalk
write_pet_names :-
    forall(
        pet(Name),
        (title_case(Name, TitleCase), write(TitleCase), nl)
    ).
```

Calling this predicate with our updated pet names table, we now get:

```text
| ?- write_pet_names.

Garfield
no
```

Our new definition fails for unexpected failures. More exactly, fails for unexpected failures in the *Test* argument. Thus, it's arguably a safer programming idiom than a traditional failure-driven loop. But it also requires the programmer to be careful, notably when splitting the goals between the *Generator* and the *Test* arguments. For example, the following innocent looking alternative is as broken as the traditional failure-driven loop it replaces:

```logtalk
write_pet_names :-
    forall(
        (pet(Name), title_case(Name, TitleCase)),
        (write(TitleCase), nl)
    ).
```

I.e. we still need to ensure there would be no unexpected failures in the *Generator* argument.
