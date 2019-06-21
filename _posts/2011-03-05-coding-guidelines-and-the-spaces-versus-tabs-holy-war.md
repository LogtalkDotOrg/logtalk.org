---
title: Coding guidelines and the spaces-versus-tabs holy war
author: Paulo Moura
layout: article
tags:
  - coding guidelines
show_edit_on_github: false
aside: false
---

Logtalk, like most programming languages, defines a set of coding guidelines that aim to improve the quality and readability of source code:

[https://logtalk.org/coding_style_guidelines.html](https://logtalk.org/coding_style_guidelines.html)

These coding guidelines are also mandatory for contributions to the Logtalk distribution. Most guidelines in the above document are pretty consensual but one of them, source code layout and indentation, always stirs a lot of discussion:

> Format your source file using tabs, not spaces. 

Search the web and you can easily find passionate texts defending the use of either tabs or spaces for source code layout and indentation. Recently, I was commenting on a [paper](http://arxiv.org/abs/0911.2899) on Prolog coding guidelines that stated:

> 2.1 Indent with spaces instead of tabs.
> 
> You cannot normally predict how tabs will be set in the editors and browsers others will use on your code. Moreover, mixing tabs and spaces makes searches and substitutions more problematic. All in all, it is better not to use tabs altogether: almost any editor can be set to substitute spaces for tabs automatically when saving your file. 

Take the first sentence. It completely misses the point of using tabs instead of spaces. Try this. Open any of the many examples distributed with Logtalk in your favorite text editor. The example source code is formatted using tabs. Next go to your text editor preferences and adjust the tab size to your liking. I prefer a tab size equivalent to 4 spaces. You may prefer a tab size equivalent to 2 spaces. Or 3 spaces. Or 6 spaces. No matter your choice, the code will remain perfectly indented. That means that I'm not imposing on you my indentation preferences. If someone gives you a file indented using spaces, say, where an indentation level is 2 spaces, and you prefer to use 4 spaces, your preference will be ignored. You will need to edit the file, i.e. change it, even if only for you to feel comfortable reading/studying the source code.

If you think that my argument is only meaningful for text editors but not for browsers, well, think again. I have written (and tested!) support for syntax highlight of Logtalk source code for Pygments, GeSHi, Highlight, Source-highlight, and SyntaxHighlighter. If you're publishing source code on a web page, a blog, or a wiki, chances are that you will be using one of these syntax highlighters. As you already guessed, they allow you to set your tab preferences. Never found a problem due to the use of tabs instead of spaces.

I have also written (and tested!) Logtalk syntax highlight support for several text editors, including TextMate, SubEthaEdit, Emacs, Vim, Kate, Gedit (i.e. GtkSourceView), NEdit, and jEdit. Again, never found a problem due to the use of tabs instead of spaces. This, I concede, may not have always been true in the past but, nowadays, using spaces for indentation is just a big waste of space. And obnoxious to all people you may share your code with that don't necessarily share with you the same preferences for the size of an indentation level.

As this post is about a holy war, it's mandatory and good netiquette that I finish it with a suitable insult or inflammatory remark to the other side. So, death to the tab infidels! May your spacebar burn in hell!
