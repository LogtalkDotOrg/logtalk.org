---
title: Lambda expressions in Logtalk
author: Paulo Moura
layout: article
tags:
  - lambdas
show_edit_on_github: false
aside: false
---

Logtalk 2.38.0, released earlier this month, adds support for [lambda expressions](http://en.wikipedia.org/wiki/Lambda_calculus). A simple example of a lambda expression is:

```text
| ?- meta::map([X,Y]>>(Y is 2*X), [1,2,3], Ys).
Ys = [2,4,6]
yes
```

In this example, a lambda expression, `[X,Y]>>(Y is 2*X)`, is used as an argument to the `map/3` list mapping predicate, defined in the library object `meta`, in order to double the elements of a list of integers. Using a lambda expression avoids writing an auxiliary predicate for the sole purpose of doubling the list elements. The lambda parameters are represented by the list `[X,Y]`, which is connected to the lambda goal, `(Y is 2*X)`, by the `(>>)/2` operator.

Currying is supported. I.e. it is possible to write a lambda expression whose goal is another lambda expression. The above example can be rewritten as:

```text
| ?- meta::map([X]>>([Y]>>(Y is 2*X)), [1,2,3], Ys).
Ys = [2,4,6]
yes
```

Lambda expressions may also contain lambda free variables. I.e. variables that are global to the lambda expression. For example, using GNU Prolog as the back-end compiler, we can write:

```text
| ?- meta::map({Z}/[X,Y]>>(Z#=X+Y), [1,2,3], Zs).
Z = _#22(3..268435455)
Zs = [_#3(2..268435454),_#66(1..268435453),_#110(0..268435452)]
yes
```

Logtalk uses the ISO Prolog construct `{}/1` for representing the lambda free variables as this representation is often associated with set representation. Note that the order of the free variables is of no consequence (on the other hand, a list is used for the lambda parameters as their order does matter).

Both lambda free variables and lambda parameters can be any Prolog term. Consider the following example by Markus Triska:

```text
| ?- meta::map([A-B,B-A]>>true, [1-a,2-b,3-c], Zs).
Zs = [a-1,b-2,c-3]
yes
```

Lambda expressions can be used, as expected, in non-deterministic queries as in the following example using SWI-Prolog as the back-end compiler and Markus Triska's CLP(FD) library:

```text
| ?- meta::map({Z}/[X,Y]>>(clpfd:(Z#=X+Y)), Xs, Ys).
Xs = [],
Ys = [] ;
Xs = [_G1369],
Ys = [_G1378],
_G1369+_G1378#=Z ;
Xs = [_G1579, _G1582],
Ys = [_G1591, _G1594],
_G1582+_G1594#=Z,
_G1579+_G1591#=Z ;
Xs = [_G1789, _G1792, _G1795],
Ys = [_G1804, _G1807, _G1810],
_G1795+_G1810#=Z,
_G1792+_G1807#=Z,
_G1789+_G1804#=Z ;
...
```

As illustrated by the above examples, Logtalk lambda expression syntax reuses the ISO Prolog construct `{}/1` and the standard operators `(/)/2` and `(>>)/2`, thus avoiding defining new operators, which is always tricky for a portable system such as Logtalk. The operator `(>>)/2` was chosen as it suggests an arrow, similar to the syntax used in other languages such as OCaml and Haskell to connect lambda parameters with lambda functions. This syntax was also chosen in order to simplify parsing, error checking, and, eventually, compilation of lambda expressions. The specification of the Logtalk lambda expression syntax can be found in the Logtalk [reference manual](https://logtalk.org/manuals/refman/grammar.html#grammar_lambdas). The current Logtalk version also includes an example, [`lambdas`](http://svn.logtalk.org/viewvc.cgi/trunk/examples/lambdas/), of using lambda expressions with a [fair number of sample queries](http://svn.logtalk.org/viewvc.cgi/trunk/examples/lambdas/SCRIPT.txt).

Although the first, experimental implementation of lambda expressions in Logtalk followed Ulrich Neumerkel's [proposal](http://www.complang.tuwien.ac.at/ulrich/Prolog-inedit/ISO-Hiord.html) for lambda expression syntax in Prolog, that representation was dropped and replaced by the current one in order to avoid some of the questions raised by the Ulrich's proposed syntax. In his proposal, lambda expressions start with the `(\)/1` prefix operator, which can be seen as an approximation to the greek letter lambda (λ). However, the backslash character is usually associated in Prolog with negation as found e.g. in the standard operators `(\+)/1`, `(\==)/2`, `(\=)/2`, and `(=\=)/2`. Another issue with this operator is that users must be careful when the first lambda parameter is enclosed in parentheses. Consider the following example by Markus (using SWI-Prolog with Ulrich's `lambda` library):

```text
| ?- maplist(\(A-B)^(B-A)^true, [1-a,2-b,3-c], Zs).
false.
```

The goal fails because there is a missing space between the `(\)/1` prefix operator and the opening parenthesis that follows. A likely trap for beginners. Ulrich's syntax for lambda free variables requires adding a new infix operator, `(+\)/1`, to the base language, something that I prefer to avoid. Not to mention that this operator is too similar to the Prolog negation operator, `(\+)/1`. Parsing lambda parameters also needs to be careful to avoid calling a non-existing `(^)/2` predicate when the lambda expression is misformed. Parsing lambda parameters is arguably simpler in Logtalk due to the use of a list plus using the `(>>)/2` operator to connect the parameters with the lambda goal.

The Logtalk implementation of lambda expressions is still evolving. The current development version features improved error-checking and adds support for using a `(>>)/2` lambda expression as a goal (besides as a meta-predicate closure). No optimizations are yet in-place. Thus, be aware of possible performance issues if you plan to use lambda expressions heavily in your applications. But don't let that stop you from having fun playing with Lambda expressions in Logtalk. As always, your feedback is appreciated. Thanks to Ulrich Neumerkel, Richard O'Keefe, and Markus Triska for their lambda expression examples.
