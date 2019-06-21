---
title: Zipper lists in Prolog
author: Paulo Moura
layout: article
tags:
  - zippers
show_edit_on_github: false
aside: false
---

I'm currently looking into zipper data structures. Searching the web for _zippering lists for prolog_, the third hit is this old blog post by Daniel Lyons (hi Daniel!):

<http://old.storytotell.org/blog/2007/08/07/list-zippers-in-haskell-and-prolog.html>

But I don't liked the calls to `reverse/2` and `append/3` and their implied performance hits. So, I just rewrote the code to eliminate the calls (and start list index at 1; this is not C! :-)

```logtalk
% zipper(+Position, +List, -Zip, -Element)
%
% where Zip = zip(Before, Element, After)
%
% index starts at 1

zipper(Position, List, Zip, Element) :-
    zipper(Position, List, [], Zip, Element).

zipper(1, [Head|Tail], Acc, zip(Acc,Head,Tail), Head).
zipper(N, [Head|Tail], Acc, zip(Before,Element,After), Element) :-
    N > 1,
    M is N - 1,
    zipper(M, Tail, [Head|Acc], zip(Before,Element,After), Element).

next(zip(Before,Element,[Head|Tail]), zip([Element|Before],Head,Tail)).

previous(X, Y) :-
    next(Y, X).
```

Some sample queries:

```logtalk
?- [zipper].
% zipper compiled 0,00 sec, 5 clauses
true.

?- zipper(3, [1,2,3,4,5], Zip, X), next(Zip, Next).
Zip = zip([2, 1], 3, [4, 5]),
X = 3,
Next = zip([3, 2, 1], 4, [5]) .

?- zipper(3, [1,2,3,4,5], Zip, X), next(Zip, Next), previous(Next, Zip).
Zip = zip([2, 1], 3, [4, 5]),
X = 3,
Next = zip([3, 2, 1], 4, [5]) .

?- zipper(3, [1,2,3,4,5], Zip, X), previous(Zip, Previous).
Zip = zip([2, 1], 3, [4, 5]),
X = 3,
Previous = zip([1], 2, [3, 4, 5]) .

?- zipper(3, [1,2,3,4,5], Three, X),
   next(Three, Four), next(Four, Five), previous(Five, Four),
   previous(Four, Three), previous(Three, Two), previous(Two, One).
Three = zip([2, 1], 3, [4, 5]),
X = 3,
Four = zip([3, 2, 1], 4, [5]),
Five = zip([4, 3, 2, 1], 5, []),
Two = zip([1], 2, [3, 4, 5]),
One = zip([], 1, [2, 3, 4, 5]) .
```

I wonder how many curious Prolog programmers wrote a similar solution in the past. A cut can be added to the first clause of `zipper/5` to eliminate a choice point. The zipper constructed is not the same (minus the index start) as in Daniel's solution, however, as we can no longer simply concatenate `Before+Element+After` to get the original list. On the other hand, my solution follows the list example on the Wikipedia page:

[http://en.wikipedia.org/wiki/Zipper\_(data\_structure)](http://en.wikipedia.org/wiki/Zipper_(data_structure))

Pros and cons of both solutions from an usage perspective? Still learning but this is fun programming :-) Eventually, I hope to add support for zipper data structures to the Logtalk library.
