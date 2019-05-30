---
layout: article
title: Easily QuickCheck your predicates at the top-level
---

Logtalk 3.25.0, released earlier today, includes a significantly improved implementation of QuickCheck supporting property-based testing of plain Prolog, Prolog module, and Logtalk object predicates. Usage is simple and can be illustrated with some examples. Below I'm using SWI-Prolog but you can use any of the Logtalk supported Prolog systems. 

Assume the following broken predicate definition: 

	every_other([], []). 
	every_other([_, X| L], [X | R]) :- 
	        every_other(L, R). 

The predicate is supposed to construct a list by taking every other element of an input list. E.g. 

	?- every_other([1,2,3,4,5,6], List). 
	List = [2, 4, 6]. 

How do we QuickCheck the predicate? Assuming Logtalk is already installed: 

	?- {lgtunit(loader)}. 
	... 

The `lgtunit::quick_check/1` predicate takes a predicate property (or signature) and runs random generated tests (100 by default): 

	?- lgtunit::quick_check(every_other(+list, -list)). 
	*     quick check test failure (at test 2 after 1 shrink): 
	*       every_other(['l!"$%}UYD_'],A) 
	false. 

Here QuickCheck reports that the predicate fails for a list with a single element. Effectively, the predicate definition is assuming an input list with an even number of elements. After finding a counter-example, the QuickCheck implementation tries to shrink it in order to report the most simple counter-example possible to facilitate debugging. For example, using the `lgtunit::quick_check/2` predicate that allows us to specify the number of tests and the maximum number of shrink operations (64 by default): 

	?- lgtunit::quick_check(every_other(+list, -list), [n(64), s(0)]). 
	*     quick check test failure (at test 2 after 0 shrinks): 
	*       eo([732,426,15,'x=mGbSI8n',-390.155545041618,A,B],C) 
	false. 

Another example: 

	foo([]). 
	foo([N| _]) :- N mod 2 =:= 0. 
	
	?- lgtunit::quick_check(foo(+list(integer)), [n(42), s(0)]). 
	*     quick check test failure (at test 4 after 0 shrinks): 
	*       nop([565,-653,784,479,755,-517,572,-869,78,-719,-175]) 
	false. 
	
	?- lgtunit::quick_check(foo(+list(integer)), [n(42), s(10)]). 
	*     quick check test failure (at test 5 after 7 shrinks): 
	*       nop([1]) 
	false. 

Let's try it again, this time with a module predicate: 

	?- use_module(library(pairs)). 
	true. 
	
	?- lgtunit::quick_check(pairs_keys_values(+list(pair(atom,integer)),-list(atom),-list(integer))). 
	% 100 random tests passed 
	true. 

There is also a `lgtunit::quick_check/3` predicate that returns results in reified form. For details about the `lgtunit::quick_check/1-3` predicates (and the QuickCheck test idioms), see: 

https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md 

For use in the predicate property/signatures, the Logtalk library makes available 89 types (several of them parameterizable), can generate arbitrary (random) values for 76 of those types, and is able to shrink values for 52 types. Also supported is the definition of type edge cases (e.g. `0` or `[]` or `''`), which are tried before resorting to generating random values. Currently, 57 edge cases for common types are defined by default. The type and arbitrary entities are user-extensible using multifile predicates. For details see: 

https://logtalk.org/library/type_0.html 
https://logtalk.org/library/arbitrary_0.html 
