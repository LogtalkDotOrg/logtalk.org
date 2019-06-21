---
title: Using both object proxies and regular objects
author: Paulo Moura
layout: article
tags: proxies
show_edit_on_github: false
aside: false
---

During the last three days I was working with Artur Miguel Dias, the author of [CxProlog](http://ctp.di.fct.unl.pt/~amd/cxprolog/), rewriting [P-FLAT](http://ctp.di.fct.unl.pt/~amd/lfa/pflat/), a Prolog toolkit for teaching Formal Languages and Automata Theory, as a Logtalk application, tentatively named L-FLAT. We made great progress and the final version of L-FLAT is going to be smaller, more portable, and both simpler to maintain and extend than the original plain Prolog application. One of our goals is to allow users to use both object proxies and regular objects when representing Turing Machines, Pushdown Automata, Context Free Grammars, and other concepts and mechanisms supported by L-FLAT. This flexibility allows users to represent e.g. a simple Finite Automaton with a small number of states and transitions as an object proxy (i.e. as a Prolog compound term; see my [previous post](../15/efficient-representation-of-data-objects.html)) that might be entered interactively at the command-line:

```logtalk
fa(fa1,
    1,                                    % initial state
    [1/a/1, 1/a/2, 1/b/2, 2/b/2, 2/b/1],  % transitions
    [2]                                   % final states
).
```

It also allows users to represent e.g. a complex Turing Machine with dozens of transitions as a regular object, defined in a source file:

```logtalk
:- object(copyTM,
    instantiates(tm)).

    initial(q0).

    transitions([
        q0/'B'/'B'/'R'/q1,
        q1/a/'X'/'R'/q2,   q1/b/'Y'/'R'/q5,   q1/'B'/'B'/'L'/q7,
        q2/a/a/'R'/q2,     q2/b/b/'R'/q2,     q2/'B'/'B'/'R'/q3,
        q3/a/a/'R'/q3,     q3/b/b/'R'/q3,     q3/'B'/a/'L'/q4,
        q4/a/a/'L'/q4,     q4/b/b/'L'/q4,     q4/'B'/'B'/'L'/q4,
                           q4/'X'/'X'/'R'/q1, q4/'Y'/'Y'/'R'/q1,
        q5/a/a/'R'/q5,     q5/b/b/'R'/q5,     q5/'B'/'B'/'R'/q6,
        q6/a/a/'R'/q6,     q6/b/b/'R'/q6,     q6/'B'/b/'L'/q4,
        q7/'X'/a/'L'/q7,   q7/'Y'/b/'L'/q7
    ]).

    finals([]).

:- end_object.
```

Using both object proxies and regular objects requires that all predicates that expect e.g. a Regular Expression to accept both an object identifier and an object proxy (a compound term) as argument. This might sound as an additional hurdle until you realize that an object proxy is also an instantiation of the identifier of a parametric object. As long as the parametric object defines the straightforward predicates that give access to its parameters, everything will work as expected. But how do we relate the regular objects and the parametric objects? Easy. If you want to represent e.g. some finite automata as instances of class `fa` and other finite automata as object proxies, simply define a parametric object as an instance of class `fa`. The parametric object parameters will be the properties that might be unique for a specific finite automaton. The parametric object define the predicates that give access to these properties. These predicates are the same that are used in class `fa` in the definition of all predicates that need access to finite automaton properties:

```logtalk
:- object(fa(_Initial, _Transitions, _Finals),
    instantiates(fa)).

    initial(Initial) :-
        parameter(1, Initial).

    transitions(Transitions) :-
        parameter(2, Transitions).

    finals(Finals) :-
        parameter(3, Finals).

:- end_object.
```

Thus, using both object proxies and regular objects becomes trivial, fully transparent, and just a matter of defining the necessary parametric objects.
