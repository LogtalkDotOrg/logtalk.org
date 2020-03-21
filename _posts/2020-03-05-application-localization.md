---
layout: article
title: Localizing an application for multiple languages
tags:
  - best practices
  - message printing
show_edit_on_github: false
aside: false
---

Applications often need to be localized in multiple natural languages. Textual
elements of an application user interface such as banners, messages, and
questions should use the native language of the user. The best practice in
this case is to decouple the application core logic from the natural language
used when interacting with the user. Customizing the application for additional
natural languages should be as simple as defining and loading the new text
translations. Moreover, applications typically allow the user to select a
language at runtime. Therefore, loading multiple language translation
resources at application startup should not be an issue.

In Logtalk and some Prolog systems, textual user interaction is preferable
handled by a [structured message printing mechanism](https://logtalk.org/manuals/userman/printing.html).
Logtalk complements message printing support with a
[question asking mechanism](https://logtalk.org/manuals/userman/printing.html#asking-questions)
for a comprehensive solution to user interaction. In this blog post, we
show how these mechanisms can be used for application localization.

As a simple example, assume that we are developing a game that prints a banner
at startup that should be localized. The game core logic prints the banner
using a `banner` message term and that is the extent of its responsibilities.
The use of message terms allows us to abstract not only how and where a message
is printed but also the actual text that will be used. But how do we specify
the language for the text? The Logtalk structured message printing API predicates
include a *component* argument that can be any bound term. This argument allows
easy partition of messages for applications made of multiple components, helping
avoiding conflicts and allowing all messages for a given component to be
handled as a set. We can use this argument to parameterize the messages
using the selected language. Assuming our game uses the compound term
`my_game(Language)` as the component identifier, the core logic could
print the banner using the following code:

```logtalk
:- object(my_game(_Language_)).

    % we use an object parameter to pass the country code
    % of the language to be used when printing messages

    :- public(banner/0).
    banner :-
        logtalk::print_message(comment, my_game(_Language_), banner).

    ...

:- end_object.
```

The [`logtalk::print_message/3`](https://logtalk.org/manuals/refman/methods/print_message_3.html)
predicate takes as arguments the message kind, the component, and the message.

We now need to be able to define the different message translations. The
translations should be independent, allowing any number of them to be
loaded at startup without conflicts and new translations to be written
without requiring changes to core logic or existing translations.
Here we can use a
[category](https://logtalk.org/manuals/userman/categories.html)
per translation. For example:

```logtalk
:- category(my_game_en_localization).

    :- multifile(logtalk::message_tokens//2).
    :- dynamic(logtalk::message_tokens//2).

    logtalk::message_tokens(banner, my_game(en)) -->
        ['Welcome to my great game!'-[], nl].

:- end_category.
```

```logtalk
:- category(my_game_pt_localization).

    :- multifile(logtalk::message_tokens//2).
    :- dynamic(logtalk::message_tokens//2).

    logtalk::message_tokens(banner, my_game(pt)) -->
        ['Bem vindo ao meu grande jogo!'-[], nl].

:- end_category.
```

```logtalk
...
```

The [`logtalk::message_tokens//2`](https://logtalk.org/manuals/refman/methods/message_tokens_2.html)
multifile non-terminal translate message terms, `banner` in this case,
into a list of tokens that define the actual message output.

At startup, the core logic can peek the language setting and call the
`banner/0` predicate as illustrated by the following queries:

```text
| ?- my_game(de)::banner.
Willkommen Sie bei Mein tolles Spiel!
yes

| ?- my_game(en)::banner.
Welcome to my great game!
yes

| ?- my_game(fr)::banner.
Bienvenue sur mon grand jeu!
yes

| ?- my_game(pt)::banner.
Bem vindo ao meu grande jogo!
yes
```

We could of course use instead a `banner(Language)` message term. But
assuming that all messages are localized, it is simpler and uniform to parameterize
the component term itself. Not a command-line text game? No problem.
We can always [abstract user interaction](../../../2019/11/14/abstracting-user-interaction.html)
using the same structured message printing and question asking mechanisms.


### Resources

This post is based on the [`localizations`](https://github.com/LogtalkDotOrg/logtalk3/tree/master/examples/localizations)
example distributed with Logtalk.
