---
title: "From casual description of Turing Machine to uncomputable functions"
date: 2024-07-31T02:36:11+08:00
draft: true
TocOpen: true
categories: ["theory-of-computation"]
tags: ['maths', 'computability-theory']
---

### Defining the machine by describing it

In Sipser's `Introduction to the theory of computation`, a alternative way of defining a Turing machine (other than defining the formal [7-tuple](https://en.wikipedia.org/w/index.php?title=Turing_machine#Formal_definition), which is a PITA) - by its "description". Example (from the proof of $A_{TM}$ is deciable): 

```
M = “On input hB,wi, where B is a DFA and w is a string: 1. Simulate B on input w. 2. If the simulation ends in an accept state, accept . If it ends in a nonaccepting state, reject .”
```

Of cause, we know that the 7-tuple definition is for the sake of formality, if we have to define and manipulate a 7-tuple machine every time we want to do something with Turing machines, that would be insanely tedious. Hence in the book (and in many other occasions?) the Turing machines are defined by its "description", including those relatively complicated ones, such as the Turing machine which can output its own description in the proof of recursion theorem.

### 

So what is the problem? In fact this approach makes sense in a great extend: not only it reduces the effort of defining a Turing machine, but it also captures the intuition "Turing machines are just programs", so defining a Turing machine is essentially defining an algorithm.

For "most of the cases"