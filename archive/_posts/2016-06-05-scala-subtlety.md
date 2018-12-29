---
title: Scala Subtlety Collection
tags: [scala, subtlety]
---

## Methods w/ or w/o parentheses

> To summarize, it is encouraged style in Scala to define methods that take no parameters and have no side effects as parameterless methods, i.e., leaving off the empty parentheses. On the other hand, you should never define a method that has side-effects without parentheses, because then invocations of that method would look like a field selection.

http://stackoverflow.com/questions/7409502/what-is-the-difference-between-def-foo-and-def-foo-in-scala

