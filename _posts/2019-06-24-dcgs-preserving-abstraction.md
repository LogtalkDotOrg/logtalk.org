---
layout: article
title: "DCGs provide a threading state abstraction: don't break it"
tags:
  - dcgs
  - best practices
show_edit_on_github: false
aside: false
---

Definite Clause Grammars (DCGs) provide a useful threading state abstraction
with countless applications in Logtalk and Prolog programming. But programmers
sometimes break this abstraction without realizing it and for no benefit.
This usually happens when using a grammar from a predicate and when calling a
predicate from a grammar. To illustrate, consider the following example found
in the Logtalk distribution:

[https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/design_patterns/logic/threading_state](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/design_patterns/logic/threading_state)

In this example, a floating-point number is converted into an integer number
using a sequence of steps:

```logtalk
steps -->
    square,
    half,
    round.
```

Each step takes an input state and applies a transformation, resulting in an
output state. The **correct** way of calling the grammar is to use the standard
[`phrase/3`](https://logtalk.org/manuals/refman/methods/phrase_3.html) built-in
predicate:

```logtalk
..., phrase(steps, Float, Integer), ...
```

The **wrong** way of doing it, breaking the DCG abstraction, is to write:

```logtalk
..., steps(Float, Integer), ...
```

Why wrong? It assumes a specific compilation solution of grammar rules to
predicate clauses, which is an implementation detail, for zero performance
gains. If you want to hide from the user that the conversion is being
performed by a grammar, than simply provide a predicate that calls the
`phrase/3` built-in predicate. For example:

```logtalk
convert(Float, Integer) :-
    phrase(steps, Float, Integer).
```

The conversion steps can be defined by either grammar rules or predicates.
In either case, we can use the [`call//1`](https://logtalk.org/manuals/refman/methods/call_1.html)
built-in meta non-terminal to avoid hard-coding assumptions about how grammar
rules are compiled into clauses. Consider the first step, which squares the
floating-point number. To define it using a grammar rule, we can write (with
the help of a [lambda expression](https://logtalk.org/manuals/userman/predicates.html#lambda-expressions)):

```logtalk
square -->
    call([Number, Double]>>(Double is Number*Number)).
```

To define it as a predicate, we can write instead:

```logtalk
square(Number, Double) :-
    Double is Number*Number.
```

Assuming all steps are implemented as predicates, our `steps//0` non-terminal
definition becomes:

```logtalk
steps -->
    call(square),
    call(half),
    call(round).
```

As with the call above to the `phrase/3` built-in predicate, the call to the
`call//1` built-in meta non-terminal is fully compiled (as the first argument
is bound) and incurs no meta-call performance penalty. But, more important,
it preserves the abstraction provide by the DCGs.

P.S. Readers familiar with DCGs likely notice that the state arguments in the
`phrase/3` predicate call are not lists of tokens as traditional but numbers.
That's an interesting topic by itself and I plan to discuss it in a forthcoming
post. Stay tuned.
