---
layout: article
permalink: performance.html
title: Performance
aside:
  toc: true
---

This page contains benchmark results for selected Prolog backends. The main
goal of this page it to give you some data for comparing predicate
performance in plain Prolog and using Logtalk objects. Benchmark results
are provided for both static code and dynamic code.

All results are given in number of calls per second. By default, the
benchmark code repeats each goal up to 100000 times in order to get more
accurate results. The exception is SICStus Prolog where a value of 1000000
was used for more accurate results.

Benchmarks run on an Apple iMac 3.8 GHz 8-Core Intel Core i7, 32GB RAM, macOS 14.7.1.

## Benchmark goals

All the tests have been performed using the `benchmarks` example
distributed with Logtalk 3.85.0, using static binding with optional
features (including events support) disabled. This provides the most
relevant scenario for comparing Logtalk performance with plain Prolog
performance. The `benchmarks` example contains loader files for easily
setting up this and other test scenarios (e.g. dynamic binding).

## Static code test goals

The `benchmarks` example provides list length and naive list reverse
predicates defined in plain Prolog, in a Prolog module, and in a Logtalk
object (predicate definitions are the same in all cases). The following
goals are used for the first two benchmark tests:

> s11: `generate_list(30, List), my_length(List, _)`
>
> s12: `generate_list(30, List), module:mod_length(List, _)`
>
> s13: `generate_list(30, List), object::length(List, _)`
>
> s21: `generate_list(30, List), my_nrev(List, _)`
>
> s22: `generate_list(30, List), module:mod_nrev(List, _)`
>
> s23: `generate_list(30, List), object::nrev(List, _)`

These benchmark tests use a list of 30 elements as an argument to the
list predicates. Increasing the list length may lead to decreasing
performance differences between plain Prolog and Logtalk as the list
length computation time starts to outweigh the overhead of the message
sending mechanism. Likewise, decreasing the list length may lead to
increasing performance differences between plain Prolog and Logtalk (up
to the point you will be closing on the Logtalk message sending
mechanism overhead when compared to plain Prolog predicate calls).
However, these tests make use of common library predicates where static
binding is easily enabled, eliminating the message sending mechanism
overheads. The next two examples deal with graph search:

> s31: `maze_solve(1, 7, _)`
>
> s32: `module:mod_maze_solve(1, 7, _)`
>
> s33: `maze::solve(1, 7, _)`
>
> s41: `graph_path(0, 4, _)`
>
> s42: `module:mod_graph_path(0, 4, _)`
>
> s43: `graph::path(0, 4, _)`

When static binding is used, the performance of each set of goals is
expected to be similar. The performance of Logtalk can be worse due to
the overhead of the extra argument added to each compiled object
predicate for carrying execution context information. This overhead
depends on the Prolog abstract machine and on the optimizations used to
pass unchanged arguments between predicate calls.

## Category test goals

Category predicates can be called using either the `::/1` or the `^^/1`
control constructs. When using the `^^/1` control construct, the lookup
for both the predicate declaration and the predicate definition begins
in *this* and is restricted to the imported categories. Depending on how
the category is compiled, Logtalk may use static binding for `^^/1`
calls, providing the same performance level as calls to local object
predicates. The following goals are used for the benchmark tests:

> c1: `leaf::obj_local`
>
> c2: `leaf::ctg_direct`
>
> c3: `leaf::ctg_self`

The `obj_local` method calls a local object predicate; the performance
of such calls is equal or close to plain Prolog. The `ctg_direct` method
uses the `^^/1` control construct to call an imported category predicate.
The `ctg_self` method uses the `::/1` message sending control construct
to call an imported category predicate. While the `^^/1` calls may use
static binding, the `::/1` calls always use dynamic binding and a lookup
caching mechanism. Note that the choice between either control construct
is not simply a question of performance as the control constructs
provide different semantics for calling imported category predicates.
All three predicates perform the same computation (generating a list of
twenty elements and calculating its length) using local predicates.

## Dynamic code test goals

Dynamic code tests include both object database updates and creating and
abolishing dynamic objects. The `benchmarks` example provides an object
named `database`, which defines a set of predicates for testing the
Logtalk built-in database methods as described below. The following
goals are used for the benchmark tests:

> d1: `create_object(xpto, [], [], []), abolish_object(xpto)`
>
> d2: `plain_dyndb(_)`
>
> d3: `database::this_dyndb(_)`
>
> d4: `database::self_dyndb(_)`
>
> d5: `database::obj_dyndb(_)`

The first test simply creates and abolishes a (dynamic) object. The
remaining tests are used for benchmarking object database updates,
comparing with plain Prolog database updates. The `*_dyndb` tests simply
assert (using `assertz/1`) and retract a clause (using `retract/1`) of a
dynamic predicate with arity one. The `plain_dyndb(_)` test uses the
Prolog built-in database predicates. The other three tests use the
Logtalk built-in database methods, using a direct method call
(`this_dyndb(_)`), a call using `::/1` (`self_dyndb(_)`), and a call
using `::/2` (`obj_dyndb(_)`).

Static code benchmark results
-----------------------------

The last columns show the trade-off between plain Prolog and Logtalk.
Dynamic binding is never used in the Prolog module tests.

## Static binding (no events support)

| Prolog compiler       |      s11      |      s12      |      s13      |    s13/s11    |
|:----------------------|--------------:|--------------:|--------------:| -------------:|
| CxProlog 0.98.3       | 475163        |      -        | 415265        | 87.4 %        |
| ECLiPSe 7.0\#57       | 2542284       | 1695466       | 2460666       | 96.8 %        |
| GNU Prolog 1.6.0      | 3571429       |      -        | 3333333       | 93.3 %        |
| SICStus Prolog 4.9.0  | 27027027      | 25641026      | 27027027      | 100.0 %       |
| SWI-Prolog 9.3.14     | 1586999       | 1559722       | 1562695       | 98.5 %        |
| Trealla Prolog 2.60.0 | 131166        | 124374        | 120015        | 91.5 %        |
| XSB 5.0.0             | 3125000       | 3030303       | 2941176       | 94.1 %        |
| YAP 7.6.0             | 1785714       | 1724138       | 1754386       | 98.2 %        |

| Prolog compiler       |      s21      |      s22      |      s23      |    s23/s21    |
|:----------------------|--------------:|--------------:|--------------:| -------------:|
| CxProlog 0.98.3       | 89545         |      -        | 85407         | 95.4 %        |
| ECLiPSe 7.0\#57       | 135901        | 122859        | 120678        | 88.8 %        |
| GNU Prolog 1.6.0      | 187617        |      -        | 198413        | 105.8 %       |
| SICStus Prolog 4.9.0  | 766284        | 732601        | 768049        | 100.2 %       |
| SWI-Prolog 9.3.14     | 84190         | 83572         | 82314         | 97.8 %        |
| Trealla Prolog 2.60.0 | 11473         | 11328         | 10520         | 91.7 %        |
| XSB 5.0.0             | 176991        | 176367        | 171527        | 96.9 %        |
| YAP 7.6.0             | 97371         | 96339         | 95785         | 98.4 %        |

| Prolog compiler       |      s31      |      s32      |      s33      |    s33/s31    |
|:----------------------|--------------:|--------------:|--------------:| -------------:|
| CxProlog 0.98.3       | 150145        |      -        | 141462        | 94.2 %        |
| ECLiPSe 7.0\#57       | 436687        | 403474        | 407477        | 93.3 %        |
| GNU Prolog 1.6.0      | 213675        |      -        | 204082        | 95.5 %        |
| SICStus Prolog 4.9.0  | 1414427       | 1342282       | 1335113       | 94.4 %        |
| SWI-Prolog 9.3.14     | 205188        | 205070        | 200929        | 97.9 %        |
| Trealla Prolog 2.60.0 | 59145         | 58214         | 52192         | 88.2 %        |
| XSB 5.0.0             | 359712        | 359712        | 346021        | 96.2 %        |
| YAP 7.6.0             | 273224        | 276243        | 255754        | 93.6 %        |

| Prolog compiler       |      s41      |      s42      |      s43      |    s43/s41    |
|:----------------------|--------------:|--------------:|--------------:| -------------:|
| CxProlog 0.98.3       | 48027         |      -        | 36524         | 76.0 %        |
| ECLiPSe 7.0\#57       | 89284         | 79597         | 84087         | 94.2 %        |
| GNU Prolog 1.6.0      | 55432         |      -        | 52521         | 94.7 %        |
| SICStus Prolog 4.9.0  | 352113        | 345185        | 354359        | 100.6 %       |
| SWI-Prolog 9.3.14     | 48796         | 40805         | 47235         | 96.8 %        |
| Trealla Prolog 2.60.0 | 14647         | 14310         | 12764         | 87.1 %        |
| XSB 5.0.0             | 97087         | 97087         | 92937         | 95.7 %        |
| YAP 7.6.0             | 59737         | 59737         | 57571         | 96.4 %        |

## Category benchmark results

The last column shows the trade-off between static binding (`c2`) and
dynamic binding (`c3`) when calling category predicates.

| Prolog compiler       |      c1       |      c2       |      c3       |    c3/c2     |
|:----------------------|--------------:|--------------:|--------------:| ------------:|
| CxProlog 0.98.3       | 227929        | 226007        | 216390        | 95.7 %       |
| ECLiPSe 7.0\#57       | 843955        | 825235        | 581380        | 70.4 %       |
| GNU Prolog 1.6.0      | 1449275       | 1449275       | 952381        | 65.7 %       |
| SICStus Prolog 4.9.0  | 4524887       | 4545455       | 2604167       | 57.3 %       |
| SWI-Prolog 9.3.14     | 496887        | 491072        | 460547        | 93.8 %       |
| Trealla Prolog 2.60.0 | 90936         | 90222         | 74027         | 82.0 %       |
| XSB 5.0.0             | 1098901       | 1075269       | 943396        | 87.7 %       |
| YAP 7.6.0             | 617284        | 598802        | 558659        | 93.3 %       |

## Dynamic code benchmark results

The last column shows the trade-off between plain
Prolog (`d2`) and Logtalk using static binding (`d3`).

| Prolog compiler       |      d1       |      d2       |      d3       |      d4       |      d5       |    d3/d2     |
|:----------------------|--------------:|--------------:|--------------:|--------------:|--------------:|-------------:|
| CxProlog 0.98.3       | 126           | 143847        | 135044        | 118913        | 122753        | 93.9 %       |
| ECLiPSe 7.0\#57       | 6868          | 970814        | 933650        | 497683        | 941957        | 96.2 %       |
| GNU Prolog 1.6.0      | 18501         | 2325581       | 2222222       | 854701        | 2127660       | 95.6 %       |
| SICStus Prolog 4.9.0  | 17269         | 2967359       | 2314815       | 1623377       | 2762431       | 78.0 %       |
| SWI-Prolog 9.3.14     | 7547          | 726475        | 678440        | 528259        | 686629        | 93.4 %       |
| Trealla Prolog 2.60.0 | 2880          | 332515        | 298230        | 205476        | 290353        | 89.7 %       |
| XSB 5.0.0             | 2535          | 318471        | 316456        | 284091        | 330033        | 99.4 %       |
| YAP 7.6.0             | 2297          | 145560        | 148810        | 131062        | 148588        | 102.2 %      |

## Remarks

-   It\'s surprisingly difficult to get stable results, specially with
    some Prolog compilers. One the reasons seems to be the
    operating-system constant shuffling of processes between the cores.
-   Some results are odd, either above the expected maximum (100% of
    plain Prolog performance) or lower than what\'s reasonable to
    expect. This happens mostly on the most simple benchmark goals.
    Benchmarks where a more significant amount of work is performed seem
    to be more (but not complete) immune to these issues.
-   All benchmark tests use the default memory allocation for the
    different program areas. Changing the size of these program areas
    can have a big impact on the benchmark results (e.g. increasing
    stack size to avoid wasting time expanding the stack or doing
    garbage collection).
-   Logtalk usually performs better with Prolog compilers with mature
    virtual machines when compared with Prolog compilers with younger
    and less optimized virtual machines. The presence, in Logtalk
    compiled code, of a hidden execution context predicate argument is a
    particular sensitive point in virtual machines optimization as this
    extra argument is usually passed unchanged between local predicate
    calls.
-   **These are too few and too limited benchmark tests to effectively
    compare Prolog compiler performance.** Notably, some of the Prolog
    versions used are development versions due to the latest stable
    version being either too old or containing critical bugs.
-   Processor caches sometimes result in tests one order of magnitude
    better than the results posted above.
-   Some of the Prolog built-in predicates used for measuring CPU time
    are not as accurate as we would like. Despite each benchmark goal
    being proved by default 100000 times, repeating the tests always
    show some variation on the final results. Increasing or decreasing
    the number of repetions may help in getting more stable results.
