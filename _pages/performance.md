---
layout: article
permalink: performance.html
title: Performance
aside:
  toc: true
---

This page contains benchmark results for some Prolog compilers. The main
goal of this page it to give you some data for comparing predicate
performance in plain Prolog and using Logtalk objects. Benchmark results
are provided for both static code and dynamic code.

## Benchmark goals

All the tests have been performed using the `benchmarks` example
distributed with Logtalk 3.16.0, using static binding with optional
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

Category predicates can be called using either the `::/1` or the `:/1`
control constructs. When using the `:/1` control construct, the lookup
for both the predicate declaration and the predicate definition begins
in *this* and is restricted to the imported categories. Depending on how
the category is compiled, Logtalk may use static binding for `:/1`
calls, providing the same performance level as calls to local object
predicates. The following goals are used for the benchmark tests:

> c1: `leaf::obj_local`
>
> c2: `leaf::ctg_direct`
>
> c3: `leaf::ctg_self`

The `obj_local` method calls a local object predicate; the performance
of such calls is equal or close to plain Prolog. The `ctg_direct` method
uses the `:/1` control construct to call an imported category predicate.
The `ctg_self` method uses the `::/1` message sending control construct
to call an imported category predicate. While the `:/1` calls may use
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

Apple MacBook Pro 15.4\" 2.9 GHz Intel Core i7, 16GB RAM, macOS 10.13.4.
All results are given in number of calls per second. By default, the
benchmark code repeats each goal up to 100000 times in order to get more
accurate results. The last columns show the trade-off between plain
Prolog and Logtalk. Dynamic binding is never used in the Prolog module
tests.

## Static binding (no events support)

| Prolog compiler              |     s11      |     s12      |     s13      |   s13/s11    |     s21      |     s22      |     s23      |   s23/s21    |     s31      |     s32      |     s33      |   s33/s31    |     s41      |     s42      |     s43      |   s43/s41    |
|:-----------------------------|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|
| B-Prolog 8.1                 | 2173913      | \-           | 2631579      | 121.1 %      | 393701       | \-           | 362319       | 92.0 %       | 564972       | \-           | 469484       | 83.1 %       | 165017       | \-           | 133869       | 81.1 %       |
| CxProlog 0.98.2              | 340702       | \-           | 308079       | 90.4 %       | 63954        | \-           | 60449        | 94.5 %       | 117756       | \-           | 110874       | 94.2 %       | 30159        | \-           | 26831        | 89.0 %       |
| ECLiPSe 7.0\#41              | 2481564      | 2003451      | 2953668      | 119.0 %      | 129298       | 124091       | 134962       | 104.4 %      | 444949       | 417162       | 404939       | 91.0 %       | 92923        | 84782        | 86275        | 92.8 %       |
| GNU Prolog 1.4.5             | 2127660      | \-           | 2777778      | 130.6 %      | 140252       | \-           | 155280       | 110.7 %      | 153139       | \-           | 143472       | 93.7 %       | 41391        | \-           | 39984        | 96.6 %       |
| Qu-Prolog 10.0               | 666667       | \-           | 588235       | 88.2 %       | 47170        | \-           | 46083        | 97.7 %       | 84746        | \-           | 81967        | 96.7 %       | 14144        | \-           | 13966        | 98.7 %       |
| SICStus Prolog 4.4.1         | 20000000     | 20000000     | 20000000     | 100.0 %      | 558659       | 561798       | 552486       | 98.9 %       | 1075269      | 1098901      | 1052632      | 97.9 %       | 278552       | 277008       | 289855       | 104.1 %      |
| SWI-Prolog 7.7.13 (64 bits)  | 772905       | 794357       | 670767       | 86.8 %       | 29531        | 29173        | 27897        | 94.5 %       | 167705       | 169819       | 159505       | 95.1 %       | 30544        | 30780        | 29901        | 97.9 %       |
| XSB 3.8.0+ (svn, 64 bits)    | 2127660      | 2631579      | 2702703      | 127.0 %      | 156495       | 155521       | 154799       | 98.9 %       | 315457       | 315457       | 303030       | 96.1 %       | 86505        | 86730        | 83752        | 96.8 %       |
| YAP 6.3.5 (git, 64 bits)     | 227273       | 225225       | 236967       | 104.3 %      | 77882        | 78186        | 75358        | 96.8 %       | 213220       | 215983       | 202020       | 94.7 %       | 41736        | 41615        | 40933        | 98.1 %       |

## Category benchmark results

All results are given in number of calls per second. By default, the
benchmark code repeats each goal up to 100000 times in order to get more
accurate results. The last column shows the trade-off between static
binding (`c2`) and dynamic binding (`c3`) when calling category
predicates.

Apple MacBook Pro 15.4\" 2.9 GHz Intel Core i7, 16GB RAM, macOS 10.13.4.

| Prolog compiler              |      c1       |      c2       |      c3       |    c3/c2     |
|:-----------------------------|--------------:|--------------:|--------------:| ------------:|
| B-Prolog 8.1                 | 1063830       | 1020408       | 666667        | 65.3 %       |
| CxProlog 0.98.2              | 161343        | 160189        | 151041        | 94.3 %       |
| ECLiPSe 7.0\#41              | 961917        | 918000        | 579907        | 63.2 %       |
| GNU Prolog 1.4.0             | 970874        | 925926        | 645161        | 69.7 %       |
| Qu-Prolog 10.0               | 232558        | 227273        | 212766        | 93.6 %       |
| SICStus Prolog 4.4.1         | 3225806       | 3030303       | 1886792       | 62.3 %       |
| SWI-Prolog 7.7.13 (64 bits)  | 253204        | 256527        | 232163        | 90.5 %       |
| XSB 3.8.0+ (svn, 64 bits)    | 1000000       | 952381        | 800000        | 84.0 %       |
| YAP 6.3.5 (git, 64 bits)     | 134953        | 132275        | 132275        | 100.0 %      |

## Dynamic code benchmark results

All results are given in number of calls per second. By default, the
benchmark code repeats each goal up to 100000 times in order to get more
accurate results. The last column shows the trade-off between plain
Prolog (`d2`) and Logtalk using static binding (`d3`).

Apple MacBook Pro 15.4\" 2.9 GHz Intel Core i7, 16GB RAM, macOS 10.13.4.

| Prolog compiler              |      d1       |      d2       |      d3       |      d4       |      d5       |    d3/d2     |
|:-----------------------------|--------------:|--------------:|--------------:|--------------:|--------------:|-------------:|
| B-Prolog 8.1                 | 10068         | 1204819       | 1098901       | 487805        | 1111111       | 91.2 %       |
| CxProlog 0.98.2              | 1889          | 47158         | 29920         | 29835         | 32284         | 63.4 %       |
| ECLiPSe 7.0\#41              | 6741          | 877645        | 837332        | 439951        | 846068        | 95.4 %       |
| GNU Prolog 1.4.5             | 12641         | 60423         | 65703         | 61050         | 64893         | 108.7 %      |
| Qu-Prolog 10.0               | 1506          | 103093        | 94340         | 84746         | 93458         | 91.5 %       |
| SICStus Prolog 4.4.1         | 12868         | 1666667       | 1587302       | 1020408       | 1562500       | 95.2 %       |
| SWI-Prolog 7.7.13 (64 bits)  | 8393          | 641363        | 611195        | 478419        | 617894        | 95.3 %       |
| XSB 3.8.0+ (svn, 64 bits)    | 2396          | 221239        | 228833        | 198807        | 224719        | 103.4 %      |
| YAP 6.3.5 (git, 64 bits)     | 2668          | 268097        | 256410        | 219298        | 259067        | 95.6 %       |

## Remarks

-   It\'s surprisingly difficult to get stable results, specially with
    some Prolog compilers. One the reasons seems to be the
    operating-system constant shuffling of processes between the cores.
-   Some results are odd, either above the expected maximum (100% of
    plain Prolog performance) or much lower than what\'s reasonable to
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
-   These are too few and too limited benchmark tests to effectively
    compare Prolog compiler performance. Notably, some of the Prolog
    versions used are development versions due to the latest stable
    version being either too old or containing critical bugs.
-   Processor caches sometimes result in tests one order of magnitude
    better than the results posted above.
-   Some of the Prolog built-in predicates used for measuring CPU time
    are not as accurate as we would like. Despite each benchmark goal
    being proved by default 100000 times, repeating the tests always
    show some variation on the final results. Increasing or decreasing
    the number of repetions may help in getting more stable results.
