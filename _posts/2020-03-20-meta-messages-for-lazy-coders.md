---
layout: article
title: Meta-messages for lazy coders
tags:
  - best practices
  - message printing
show_edit_on_github: false
aside: false
---

One of the frequent excuses for coders to avoid using the message printing
mechanism is that they require defining tokenization rules for the messages
and that is too much work when they can just call `write/1` instead. We can
try to argue about laziness but the coders do have a point. To easy the pain
of using the message printing mechanism, Logtalk defines a set of
[*meta-messages*](https://logtalk.org/manuals/userman/debugging.html#meta-messages)
that can be used without defining any `message_tokens//2` tokenization rules.
Some examples:

```text
| ?- logtalk::print_message(comment, core, @'Phase 1 completed').
% Phase 1 completed
yes

| ?- logtalk::print_message(comment, core, answer-42).
% answer: 42
yes

| ?- logtalk::print_message(comment, core, 'Position: <~d,~d>'+[42,23]).
% Position: <42,23>
yes

| ?- logtalk::print_message(comment, core, [arthur,ford,marvin]).
% - arthur
% - ford
% - marvin
yes

| ?- logtalk::print_message(comment, core, names::[arthur,ford,marvin]).
% names:
% - arthur
% - ford
% - marvin
yes
```

A second complain is that the goals are verbose. Sure, we can use implicit
message sending to the built-in `logtalk` object using the directive to
shorten the goals a bit. For example:

```logtalk
:- uses(logtalk, [
    print_message/3
]).

enterprise :-
    print_message(comment, core, @('Entering the Neutral Zone...')),
    ...,
    print_message(comment, core, @('Looking for Romulans...')),
    ....
```

But we still need to write the message *kind* and *component* arguments. Not
conceding defeat, [*predicate aliases*](../../01/08/object-and-predicate-aliases.html)
to the rescue:

```logtalk
:- uses(logtalk, [
    print_message(comment, core, @Message) as log(Message)
]).

enterprise :-
    log('Entering the Neutral Zone...'),
    ...,
    log('Looking for Romulans...'),
    ....
```

while still benefiting from all the advantages of using the
[message printing mechanism](https://logtalk.org/manuals/userman/printing.html) (see e.g. [Abstracting user interaction](../../../2019/11/14/abstracting-user-interaction.html)).

Do you happen to have some existing code using e.g. `format/2` for writing messages
that you want to port to the message printing mechanism? Note that you can write:

```logtalk
:- uses(logtalk, [
    print_message(comment, core, Format+Arguments) as format(Format, Arguments)
]).

enterprise(Zone, Enemy) :-
    format('Entering the ~w...', [Zone]),
    ...,
    format('Looking for ~w...', [Enemy]),
    ....
```

In this case, all `format/2` goals will be compiled as `logtalk::print_message/3`
goals. You could use similar aliases for other output predicates, simplifying the
port by minimizing the changes required.

P.S. The `Format+Arguments` meta-message exemplified above is implemented in
Logtalk 3.37.0, currently in development and expected to be released in April.
