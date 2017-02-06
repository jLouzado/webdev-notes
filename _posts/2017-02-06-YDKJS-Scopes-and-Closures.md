---
layout: post
title:  "Scopes and Closures"
date: 2017-02-06 09:00:00 +0530
categories: ydkjs javascript
description: You Don't Know JS - Book 2 Notes What is scope, Compiler Theory...
---

# Preface:
Same as in 'up and going'. I suspect it's the same across all the books.

# Chapter 1:

## What is scope?

- languages need variables, and the ability to store and retrieve.
    - Store and recall of variables is composes the programs state.
- Where do variables live though, where do they get stored and how does the program (you're writing) find them when they're needed.
- There's a ruleset that determines where the variables lives and how it's to be found and identified, those rules are called Scope.
- So where do the Scope rules get set?


## Compiler Theory

- Javascript is actually a compiled language even though it's categorized as an interpreted/dynamic one.
    - It's just that it's not compiled way in advance, it's done right before execution.
- Compilation is usually three steps
    - Tokenizing/Lexing - converting a program into an array of tokens. `var a = 2;` contains `var`, `a`, `=` and `2`
    - Parsing - converting the stream of symbols into a nested tree.
    - Code-Gen - converting the tree into the actual machine instructions to actually conduct those operations.
    - In addition there are some optimization steps (and lots of other things) but these are the broad strokes.
- The big difference is that the JS engine doesn't have the luxury of time for optimizations since it has to be ready to execute almost immediately.


## Understanding Scope

Scope can be understood as a conversation.

### The Cast

1. _Engine_ : responsible from start to finish for compilation nad execution
2. _Compiler_ : handles dirty work of parsing and code-gen,
3. _Scope_ : Collects and maintains a lookup list of all declared identifiers and enforces access rules for the currently executing code.

### Back & Forth

- 



























