---
title: Structured Message Printing
author: Paulo Moura
layout: article
tags:
  - best practices
show_edit_on_github: false
aside: false
---

Logtalk 3.x adds a _structured message printing_ mechanism. This feature gives the programmer full control of message printing, allowing it to filter, rewrite, or redirect any message. The origins of the mechanism for message printing that inspired the Logtalk implementation go back to Quintus Prolog, where it was implemented, apparently, by Dave Bowen (thanks to Richard O'Keefe for the historical bits). This mechanism can also be found currently on e.g. SICStus Prolog, SWI-Prolog, and YAP.

Why a mechanism for printing messages? Consider the different components in a Logtalk application development and execution. At the bottom level, you have the Logtalk compiler and runtime. The Logtalk compiler writes messages related to e.g. compiling and loading files, compiling entities, compilation warnings and errors. The Logtalk runtime writes banner messages and handles execution errors that may result in printing human-level messages. The development environment can be console-based or you may be using a GUI tool such as PDT. In the latter case, PDT needs to intercept the Logtalk compiler and runtime messages to do its magic and present the relevant information using its GUI. Then you have all the other components in a typical application. For example, your own libraries and third-party libraries. The libraries may want to print messages on its own, e.g banners, debugging information, or logging information. As you assemble all your application components, you want to have the final word on which messages are printed, where, an in what conditions.

The Logtalk message printing mechanism provides you with a set of predicates, defined in the `logtalk` built-in object, and some hook predicates. Two of the most important predicates are `logtalk::print_message(Kind, Component, Term)`, which is used for printing a message, and `logtalk::message_hook(Term, Kind, Component, Tokens)`, a user-defined hook predicate used for intercepting messages. The `Kind` argument is used to represent the nature of the message being printed. It can be e.g. a logging message, a warning message or an error message, In Logtalk this argument can be either an atom, e.g. `error`, or a compound term, e.g. `information(requested)`. Using a compound term allows easy partitioning of messages of the same kind in different groups. Messages are represented by atoms or compound terms, handy for machine-processing, and converted into a list of tokens, for human consumption. This conversion is performed using the non-terminal `logtalk::message_tokens(Term, Component)`. A simple example is:

```logtalk
:- multifile(logtalk::message_tokens//2).
:- dynamic(logtalk::message_tokens//2).

logtalk::message_tokens(loaded_settings_file(Path), core) -->
    ['Loaded settings file found on directory ~w'-[Path], nl, nl].
```

The `Component` argument is new in the Logtalk implementation and is useful to filter messages belonging to a specific component (e.g. the Logtalk compiler and runtime is identified by the atom `core`) and also to avoid conflicts when two different components define the same message term (e.g. `banner` seems to be popular).

There are also predicates for printing a list of tokens, `logtalk::print_message_tokens(Stream, Prefix, Tokens)`, for printing an individual token, `logtalk::print_message_token(Stream, Token)`, and for setting default output stream and message prefixes, `logtalk::message_prefix_stream(Kind, Component, Prefix, Stream)`. For example, the SWI-Prolog adapter file uses the `print_message_token/2` hook predicate to enable coloring of messages printed on a console.

Using the message printing mechanism in your applications and libraries is easy. Simply chose a component name for your application, call `logtalk::print_message/3` for every message that you may want to print, and define default translations for your message terms using the multifile non-terminal `logtalk::message_tokens/2`. For a full example, see e.g. the [`lgtunit` tool](https://github.com/LogtalkDotOrg/logtalk3/tree/master/tools/lgtunit "lgtunit tool"). Happy coding!
