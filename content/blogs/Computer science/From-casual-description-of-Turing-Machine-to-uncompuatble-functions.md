---
title: "From casual description of Turing Machine to the density of uncomputable functions"
date: 2024-08-09T01:23:55+08:00
TocOpen: true
categories: ["theory-of-computation"]
tags: ['maths', 'computability-theory']
math: true
---

### Defining the machine by describing it

In Sipser's `Introduction to the theory of computation`, a alternative way of defining a Turing machine (other than defining the formal [7-tuple](https://en.wikipedia.org/w/index.php?title=Turing_machine#Formal_definition), which is a PITA) - by its "description". Example (from the proof of $A_{TM}$ is deciable): 


> M = “On input <B, w>, where B is a DFA and w is a string: 1. Simulate B on input w. 2. If the simulation ends in an accept state, accept . If it ends in a nonaccepting state, reject .”


Of cause, we know that the 7-tuple definition is for the sake of formality, if we have to define and manipulate a 7-tuple machine every time we want to do something with Turing machines, that would be insanely tedious. Hence in the book (and in many other occasions?) the Turing machines are defined by its "description", including those relatively complicated ones, such as the Turing machine which can output its own description in the proof of recursion theorem.

There is seemingly no restriction of how should a description looks like, so I can create a Turing machine by literally any description, right?

![](/From-casual-description-of-Turing-Machine-to-uncompuatble-functions/right-meme.png)

### Unicorn algorithm

So what is the problem? In fact this approach makes sense in a great extend: not only it reduces the effort of defining a Turing machine, but it also captures the intuition "Turing machines are just programs", so defining a Turing machine is essentially defining an algorithm.

For "most of the cases" this is a safe and good way to deal with Turing machines. But let's consider the following description:


> M = “On input w, give a candy to the unicorn who lives in the Hilbert Grand Hotel. If the unicorn accepts your candy, accept. Otherwise reject .”


This is a description right? Does that mean I created a Turing machine and I can call it the unicorn algorithm?

Well, this is an extreme example, but the point is, the description approach of defining Turing machine is too broad, how can we make sure what we described is not "impossible"? By "possible" description, I mean a description that can be computed by a Turing machine, instead of things that cannot be done by Turing machine like ffering a candy to the unicorn. Note that there are some problems that looks pretty sane, but they are beyond the Capability of Turing machines, such as the [Busy Beaver problem](https://en.wikipedia.org/wiki/Busy_beaver).

OK, so what we need is to make sure that what the description is describing can actually be done by a Turing machine, right? Let's call such descriptions as "Turing description". But how can we tell? Can we prove/ disprove that? It is also natural to ask: "how many Turing description are there?", or the a bit more precise and interesting rephrasing: "If I pick a description randomly, how possible is it to be Turing description?"

Unfortunately, we can't. 

First of all, by "prove/ disprove", it means that we have a step-by-step, mechanical way to deduce its trueness - which means there should be a Turing machine taking the statement as input and return 0 or 1. And this Turing machine has to be a decider if we want to tell whether any given description can be implemented by some Turing machine. Let's call this decider be `D` and we will show its existence.

Let's restrict the space of possible description without loss of generality: The description of must be well-defined, as in for any given input, it can tell you whether it accepts or not. (Obviously - otherwise it does not even tell me what does it accept. Note that it is different from assuming it is describing a decider - the description just tells you the result, it does not imply that if you throw an input into the corr. Turing machine (if it exists) the machine will halt.). We also assume takes inputs that Turing machines can take (sure, otherwise we know that is not describing a Turing machine straight away).

Now note that Turing machine input can be encoded as natural numbers:

> Let the Turing machine be associated with a set of symbols $\Gamma$ and $|\Gamma| = N$. Assign numbers $0, 1, 2, \dots, N-1$ to the symbols. 
> Now the input of tape can be viewed as a N-adic number with the first symbol as the least significant figure. For example when $N = 2$, $0101$ is mapped to $1010_{2} = 10$. Note that this is a bijection between all possible input and $\mathbb{N}$.

> Also Note that the existence of blank symbol does not affect our argument, we can simply put it in $\Gamma$ and consider it as a normal symbol.

Hence a description defined above has implicitly defined a function $f:\mathbb{N} \to \{0, 1\}$ as $0, 1$ represents accept and reject.

Now, we all know that the set of all possible `f` is uncountable, and that a given Turing machine can only take countably many distinct input, we can conclude that `D` does not exist, as it cannot even take all the input that it should take, which is the set of all well-defined description, which is `f`.

### Is it really...MOST of the cases?

The answer of "If I pick a description randomly, how possible is it to be Turing description?" should be clear now - "almost every function from $\mathbb{N}$ to $\{0, 1\}$ is not Turing description, since there are uncountably many functions from $\mathbb{N}$ to $\{0, 1\}$, but only countably many Turing machines". This statement trigger a person with mathematics background: "So... does that mean the set of Turing descriptions is of measure zero in the set of functions from $\mathbb{N}$ to $\{0, 1\}$". But what is the measure of the set of all functions from $\mathbb{N}$ to $\{0, 1\}$?

I didn't find any articles discussing such measures after a few casual Google searches. We can consider the as a subspace of [Baire space](https://en.wikipedia.org/wiki/Baire_space_(set_theory)) and take the "common prefix metric" i.e. given $x=\{x_1, x_2, \dots\}$ and $y=\{y_1, y_2, \dots\}$, $d(x, y) = 0$ if $x=y$, otherwise $d(x, y) = 1/k$ where $k$ is the smallest integer s.t. $x_k \neq y_k$. 

In this metric space, the set of Turing descriptions is of (Hausdorff) measure zero: Every Turing description can be covered by an arbitrarily small $k$-ball with it as the center.

This looks trivial. Now we want to ask, is non-Turing description dense in Baire space?

Our intuition tells us that it should true. If you pick a $n$ and flip the value of $f(n)$ of a Turing description, this whole function looks "unreasonble" now and it would be drastically harder to compute. Now let's check if our Baire space model matches this intuition:

Suppose the set of non-Turing description is not dense. Then there exists a $f$ in Baire space where $f$ is Turing description s.t. there exists an open ball $B_{1/k}(f)$ s.t. no non-Turing description are in this open ball. But now all element in this open ball are Turing description. Note that there are uncountably many elements in this open ball (since the elements inside are sequences of natural numbers that the first $k$ elements are the same as those of $f$. This whole set is bijective to the whole Baire space and hence uncountable), which means there are uncountably many Turing descriptions in the open ball - which is absurd and we have a contradiction. Hence set of non-Turing description is dense.

So, now we can say that Turing descriptions are very rare that almost all functions are not Turing description.

### Outro

We have shown that defining a Turing machine by writing down its description can be wrong even when we assume the description is "well-formed". As almost every description we write is not Turing description and hence constructing complicated description and just presume that there is a Turing machine for it is problematic.

Turing descriptions is different from compuatble functions (the Turing machine corr. to a computable function is a decider) and Turing recognizable languages (there could be a Turing machine for a corr. description but it does not halt on every input that the description accepts), but computable functions can be injectively mapped into a subset of the set of Turing machines. Hence we can say that **almost every function is uncomputable and the set of uncomputable functions is dense**.

Study the space of computable functions or other computational objects in topological/ measure theoretical setup would be interesting.