---
layout: article
title: Abstracting user interaction
tags:
  - best practices
  - message printing
show_edit_on_github: false
aside: false
---

Logtalk and some Prolog systems provide a
[message printing mechanism](https://logtalk.org/manuals/userman/printing.html)
that allows abstracting the message text, where the message is effectively
printed, and how. Another key aspect of this mechanism is that a call to
print a message can be *intercepted* by defining a
[hook predicate](https://logtalk.org/manuals/glossary.html#term-hook-predicate).
Logtalk complements the message printing mechanism by providing also a
[question asking mechanism](https://logtalk.org/manuals/userman/printing.html#asking-questions).
Asking a question can also be intercepted by defining a hook predicate.
This blog post illustrates the versatility of these hook predicates to
abstract user interaction by using as example [Douglas Adams](https://en.wikipedia.org/wiki/Douglas_Adams)
ultimate question in his book
["The Hitchhiker's Guide to the Galaxy"](https://en.wikipedia.org/wiki/The_Hitchhiker%27s_Guide_to_the_Galaxy).
Jumping head first into the code:

```logtalk
:- category(hitchhikers_guide_to_the_galaxy).

    :- multifile(logtalk::message_tokens//2).
    :- dynamic(logtalk::message_tokens//2).

    % abstract the question text using the atom ultimate_question
    % the second argument, hitchhikers, is the application component
    logtalk::message_tokens(ultimate_question, hitchhikers) -->
        ['The answer to the ultimate question of Life, The Universe and Everything is?'-[], nl].

    :- multifile(logtalk::question_prompt_stream/4).
    :- dynamic(logtalk::question_prompt_stream/4).

    % the prompt is specified here instead of being part of the question text
    % as it will be repeated if the answer doesn't satisfy the question closure
    logtalk::question_prompt_stream(question, hitchhikers, '> ', user_input).

:- end_category.
```

The [`logtalk::message_tokens//2`](https://logtalk.org/manuals/refman/methods/message_tokens_2.html)
non-terminal defines how to convert the abstract representation of the message
text (the atom `ultimate_question`) into tokens. The
[`logtalk::question_prompt_stream/4`](https://logtalk.org/manuals/refman/methods/question_prompt_stream_4.html)
predicate defines a prompt and an input stream. Asking a question implies
printing a message (the question text after tokenization), and reading
a reply. After loading this category, we can ask the question using the [`logtalk::ask_question/5`](https://logtalk.org/manuals/refman/methods/ask_question_5.html)
predicate:

```text
| ?- logtalk::ask_question(question, hitchhikers, ultimate_question, '=='(42), N).

The answer to the ultimate question of Life, The Universe and Everything is?
> 42.

N = 42
yes
```

Note the `'=='(42)` argument, a closure that is used to check the user answer
to the question. The question is repeated until the goal constructed from that
that closure and the user answer succeeds. For example:

```text
| ?- logtalk::ask_question(question, hitchhikers, ultimate_question, '=='(42), N).

The answer to the ultimate question of Life, The Universe and Everything is?
> icecream.
> tea.
> 42.

N = 42
yes
```

So far, we relied on the default behavior for the message printing and question
asking mechanisms. All user interaction occurred at the top-level interpreter.
This is fine when developing and manually testing. But deployed applications
usually don't include a top-level interpreter and testing is preferably
automated. But how do we divert the question to e.g. a GUI interface and how
do we automate testing of code where one of the steps is asking a user a
question and waiting for its reply?

### From top-level interpreter to GUI interface

We now want to divert the question and user answer to a GUI interface. For
example, a GUI dialog. This can be easily accomplished by using the
[`logtalk::question_hook/6`](https://logtalk.org/manuals/refman/methods/question_hook_6.html)
hook predicate. As there are no standard solutions for Prolog GUI interfaces
that we can use from Logtalk, we need to make a hard choice here. To continue
our example, we're going to use a Java-based interface that you can play with
using JIProlog, SWI-Prolog, or YAP as the backend. An alternative would be to
use a web interface but that we would also restrict the compatible backends.

```logtalk
:- category(gui).

    :- multifile(logtalk::question_hook/6).
    :- dynamic(logtalk::question_hook/6).
    :- meta_predicate(question_hook(*, *, *, *, 1, *)).

    logtalk::question_hook(ultimate_question, _, hitchhikers, Tokens, Check, Answer) :-
        tokens_to_text(Tokens, Question),
        java('javax.swing.JFrame')::new(['The Hitchhiker''s Guide to the Galaxy'], Frame),
        % repeat the question until we get the correct answer
        repeat,
            java('javax.swing.JOptionPane', Answer0)::showInputDialog(Frame, Question),
            atom_codes(Answer0, Codes),
            catch(number_codes(Answer, Codes), _, fail),
        call(Check, Answer),
        !,
        java(Frame)::dispose.

    % just a hack for this example
    tokens_to_text([Question-[], _], Question).

:- end_category.
```

This category uses the Logtalk [`java`](https://logtalk.org/library/library_index.html#java)
library that abstracts interfacing with Java. As we're no longer relying on
default behavior, we use here a repeat loop to present the dialog to the
user until the correct answer is typed. By simply loading this category,
asking the question again will present the following dialog:

![Dialog](/blog_images/abstracting_user_interaction_dialog.png "Dialog")

Note that this switch from a command-line interaction to a GUI interaction
doesn't require any changes to the `logtalk::ask_question/5` calls. In
actual applications, this means that **we can switch the user interface
without any changes to the core application calls that print messages and
ask questions**.

### Automating user interaction for testing

To automate testing, we simply use the `logtalk::question_hook/6` predicate to
provide a **fixed** answer. For example, we can provide the correct answer:

```logtalk
:- category(hitchhikers_fixed_answers).

    :- multifile(logtalk::question_hook/6).
    :- dynamic(logtalk::question_hook/6).

    logtalk::question_hook(ultimate_question, question, hitchhikers, _, _, 42).

:- end_category.
```

In a practical case, the fixed answers would be used for followup goals being
tested. As mentioned before, the question answer read loop (which calls the
question check closure) is not used when a fixed answer is provided (using the
`logtalk::question_hook/6` predicate) thus preventing the creation of endless
loops. With the `hitchhikers_fixed_answers` category compiled and loaded, we
can now define a couple of tests for our example:

```logtalk
:- object(tests,
    extends(lgtunit)).

    test(questions_01, true(N == 42)) :-
        logtalk::ask_question(question, hitchhikers, ultimate_question, '=='(42), N).

    test(questions_02, true(N == 42)) :-
        logtalk::ask_question(question, hitchhikers, ultimate_question, '=='(41), N).

:- end_object.
```

The tests can now run automated without any user interaction:

```logtalk
| ?- {tester}.
% 
% tests started at 2019/11/14, 11:17:38
% 
% running tests from object tests
% file: logtalk3/examples/questions/tests.lgt
% 
% questions_01: success
% questions_02: success
% 
% 2 tests: 0 skipped, 2 passed, 0 failed
% completed tests from object tests
% 
% no code coverage information collected
% tests ended at 2019/11/14, 11:17:38
% 
yes
```

### Resources

This post is based on the [`questions`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/questions)
example distributed with Logtalk. A related example is
[`localizations`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/localizations),
which illustrates how to use the message printing mechanism to provide
software localization in several natural languages.
