---
title: "The double dual trick to construct a better object from the existing one"
subtitle: "Stone–Čech compactification and group abelianization"
math: true
tikz: true
date: 2025-07-31T23:28:34+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['group-theory', 'topology', 'category-theory', 'algebra']
---

### Stone–Čech compactification

One of the proof of the Stone–Čech compactification is to consider the continuous functions from a given topological space $X$ to $[0, 1]$.

Crux 1: constructing $[0, 1]^{C}$

Let $C$ be the space of all continuous functions from $X$ to $[0, 1]$, consider $[0, 1]^{C}$, there is a natural map from $X$ to $[0, 1]^{C}$: for each $x \in X$, define $\phi(x) = f \mapsto f(x)$. With product topology $\phi$ is continuous. Also by Tychonnof's theorem $[0, 1]^{C}$ is compact. Now the closure of the image is obviously compact Hausdorff, and it satisfies a nice property: any continuous map $f : X \to [0, 1]$ extends uniquely to a continuous map $\overline{\phi(X)} \to [0,1]$: for any $\phi(x)$, it has to map to $f(x)$!

Crux 2: $[0, 1]^{C}$ is a cogenerator of the category of compact Hausdorff space

$[0, 1]^{C}$ is a cogenerator, i.e. for any distinct maps of compact Hausdorff spaces $f, g : A \to B$, there is a map $h: B \to [0, 1]^{C}$ such that $hf$ and $hg$ are also distinct. Now it is clear that any continuous map $f : X \to K$ where $K$ is a compact Hausdorff space actually extends uniquely to $\overline{\phi(X)} \to K$, since otherwise we would be able to construct distinct maps from $\overline{\phi(X)} \to [0,1]$.

...

My first thought after learning this is: **Why does the setup look so familiar with double dual space?!**


### Natural map to the double dual of a vector space

Let $V$ be a vector space of a field $k$, the dual of $V^*$ is the space of linear functionals $V \to k$. The double dual $V^{\*\*}$ is the space of linear maps that send linear functionals to $k$. There is a natural map $\phi$ from $V$ to $V^{\*\*}$: let $v \in V$, for any $L \in V^{\*}$ define $\phi(v) = L \mapsto L(v)$.

If you interpret this in an a bit generalized setup, you can think of it as the following with the minimum amount of categorical language:

Given an category $X$, find a good object $A$ and construct the category $Y$ which has objects $f: X \to A$ and consider the functor from $X$ to $Y$. Now look at how $X$ is embedded in $Y$, it may share some nice properties of $Y$.

In the construction of Stone–Čech compactification, we consider the maps from the space $X$ to a compact Hausdorff space $C$, construct the canonical map from $X$ to the "double dual" (maps from (the maps from $X$ to $C$) to $C$), then we notice that the (closure of the) image is very nice, and turns out it is the universal object we are looking for.

This actually provides an interesting way to think about a structured object as mappings with (not necessarily the same) structure - it is like a way to "push" something into another category out of thin air!

This trick should work in wider scope, not just for topology, because the whole idea is about finding a good object and consider the maps to it, embedding the object to the double dual!

Below is a fun way I come up with to think about a classic topic in group theory: abelianization of a group, although the universal property we prove is not an extension, but a "descend".


### Group abelianization

The classical way to introduce group abelianization is by introducing the **commutator** of a group $[G, G] = \{g^{-1}h^{-1}gh: g, h \in G\}$ followed by proving that it is a normal subgroup of $G$ and proving that the quotient is abelian. But isn't the task "universally adding an extra structure to an object" same with what Stone–Čech compactification does? Why not try the same trick on groups and abelian groups?

Let $A = \mathbb{Q}/\mathbb{Z}$. Note that $A$ is a cogenerator in the category of abelian groups by the following:

**Lemma 1**\
For any $x \neq e$ in an abelian group, there is a $\phi$ such that $\phi(x) \neq 0$. In fact, let $n$ be the order of $x$, if $n$ is finite we can map it to $\frac{1}{n}$ and everything else to 0; if $n$ is infinite then $\langle x \rangle \cong \mathbb{Z}$, we can also map $x$ to $\frac{1}{n}$, this is a homomorphism since it is essentially $\mathbb{Z} \to \mathbb{Z}/n\mathbb{Z}$

**Corollary 1**\
For any distinct element $x, y$ in an abelian group $G$, there is a homomorphism $\phi: G \to A$ such that $\phi(x) \neq \phi(y)$. Hence $A$ is a cogenerator.

Now we are ready to do the abelianization.

Given a (not necessarily abelizan) group $G$, consider $Hom(Hom(G, A), A)$ where $Hom(X, Y)$ of groups $X, Y$ is the set of homomorphism from $X$ to $Y$. It can be seen that $Hom(G, A)$ is an abelian group by defining $\phi \dot \psi (g) = \phi(g) \dot \psi(g)$. Hence $Hom(Hom(G, A), A)$ is also an abelian group.

Now consider the natural map $F: G \to Hom(Hom(G, A), A)$ defined by $F(g) = \phi \to \phi(g)$  $\forall \phi \in Hom(Hom(G, A), A)$. It is easy to check that $F$ is a group homomorphism. And $F(G)$ is abelian as a subgroup of an abelian group.

Now since $F(G) \cong G/ker(F)$ every homomorphism $\phi: G \to A$ descends to a unique abelian group homorphism $\~{\phi}: F \to A$ through the canonical projection.

Next we need to show that $ker(F) = [G, G]$. Note that $x \in ker(F) \iff \phi(x) = 0$   $\forall \phi \in Hom(G, A)$

First $[G, G] \subseteq ker(F)$ since $\phi(g^{-1}h^{-1}gh) = \phi(g^{-1}gh^{-1}h) = \phi(e) = 0$ for any $\phi$ (the image being in an abelian group is useful here).

For the converse, note that $\phi$ is a process of "forgetting the order of multiplication in $G$": $\phi(xy)=\phi(x)\phi(y) = \phi(y)\phi(x) = \phi(yx)$. So by lemma 1, if $x$ is in $ker(F)$ it is equal to $e$ after "forgetting the order of multiplication", so it can be written in $yy^{-1}$ for some $y \in G$ after "organizing the factors". However $yy^{-1} = e$ in $G$, which we already know is in $ker(F)$. So for $y \neq e$ we choose a $g \neq e \in G$, we write $y = gh$ where $h = g^{-1}$. Now by reorganizing the factors we have shown that $x = g^{-1}h^{-1}gh$. 

QED.


### Summary: when is the double dual trick useful?

Let's say you want to add some structure to an existing object.

First you need a cogenerator. Then you need a structure that is good enough to occur in the double dual such that the natural map to the double dual preserves the structure. Now it is very likely for it to going to work.

Such a powerful trick :slightly_smiling_face: