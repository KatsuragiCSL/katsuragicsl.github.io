---
title: "Amazed by how ring theory can be linked up to geometry"
date: 2025-05-13T00:03:17+08:00
draft: true
math: true
tikz: true
TocOpen: true
categories: ["mathematics"]
tags: ['algebra', 'geometry', 'algebraic geometry']
cover:
  image: "https://upload.wikimedia.org/wikipedia/commons/2/25/Squarecubetesseract.png"
---

I am reviewing some fundamental algebra, and I just learnt something beautifully suggesting the connection of ring theory and geometry, which made me eager to learn some algebraic geometry (which I was not very interested when I was in undergrad). It is an exercise in Aluffi's book[^1].

Lets' jump into it.

### The problem
Let $K$ be a compact topological space, and let $R$ be the ring of continuous real-valued functions on $K$, with addition and multiplication defined pointwise. \
(i) For $p \in K$, let $M_p = \\{f \in R | f(p) = 0\\}$. Prove that $M_p$ is a maximal ideal in $R$. \
(ii) Prove that if $f_1, \dots , f_r \in R$ have no common zeros, then $(f1, \dots , fr)$ = $(1)$. \
(Hint: Consider $f^2_1 + \dots + f^2_r$ .) \
(iii) Prove that every maximal ideal $M$ in $R$ is of the form $M_p$ for some $p \in K$. \
(Hint: You will use the compactness of $K$ and (ii).)

Conclude that $p \mapsto M_p$ defines a bijection from $K$ to the set of maximal ideals
of $R$.

...and for a complete picture, here is a related problem [^2] (also in the same book) to show that compactness of $K$ is necessary:

> Let $R$ be the ring of continuous from $\mathcal{R}$ to $\mathcal{R}$. Show that there is a maximal ideal of $R$ such that it is not in the form of $M_p$.


### Thought process
(i) is trivial by constructing a ring homomorphism $\phi$ from $R$ to $\mathcal{R}$ such that $\phi (f) = f(p)$.

(ii) is also straight forward: \
First notice that $1$ in $R$ is the function $Id$ on $K$ such that $Id(x) = 1 \forall x \in K$. So for any $f \in R$ if $f$ has no zeros it will have an inverse ($\dfrac{1}{f}$). So what happens if $f_1, \dots , f_r \in R$ have no common zeros? They can "cover" each other. Though it is not simply $f_1 + \dots + f_r$ since the "positive plus negative" cases will cause pathologies. But $f^2_1 + \dots + f^2_r$ obviously solve this problem: it is always positive. And hence has an inverse. Since the ideal $(f1, \dots , fr)$ contains $f1, \dots , fr$, it must contains $f^2_1 + \dots + f^2_r$ and hence the ideal equals to the whole $R$.

(iii) is a little bit tricky, but is the beautiful part of the problem. Below is a rough recap of my thought process:

First, from (ii) one should expect that $M$ cannot contains functions with no common zeros, otherwise $M = R$. So maybe let denote $Z$ as the set of common zeros of all the functions in $M$? What does this $Z$ should look like? It is natural to expect that it is non-empty. We want it to be a singleton because that will match the definition of $M_p$. We hope $M = \\{f \in R | f(Z) = 0\\}$ and $Z$ is a singleton, that seems natural and it will prove the statement straight away.

But...what if it is not? What will happen if there are more than one common zeros...? Oh actually it does not matter, since obviously $\\{f \in R | f(Z) = 0\\} \subseteq \\{f \in R | f(p) = 0\\}$ for any $p \in Z$, and since $M$ has to be maximal so as long as we can show $M \subseteq \\{f \in R | f(Z) = 0\\}$ it immediately implies that $M \subseteq \\{f \in R | f(p) = 0\\}$ for some $p \in Z$.

Ok, is it even possible for $M$ to be not contained in $\\{f \in R | f(Z) = 0\\}$...? It seems impossible, cuz the functions in $M$ must have common zeros or $M$ will eqaul to $R$. Hence any function $f \in M$ must also be in $\\{f \in R | f(Z) = 0\\}$ right...? Huh? Isn't that complete the proof? But I didn't use the compactness of $K$. I should expect it fails when $K$ is not compact, so let's think about a counterexample...

\[After trying to construct a few functions from $\mathcal{R}$ to $\mathcal{R}$ and let them generate an ideal so that the resulting ideal is not contained in $\\{f \in R | f(p) = 0\\}$ for some $p \in \mathcal{R}$, but with no luck, I turn into the following thoughts...\]

It seems hard to imagine the statement is not true for general $K$, I must have done something wrong... Let's look at (ii) again since it causes all the pathologies. Oh wait, it says $f_1, \dots , f_r \in R$ should have common zeros, there are only finitely many of them! So in order to fail one must construct a collection of continuous functions such that any finite subcollection of them have common zeros, but the whole collection of them have no common zeros. Looking at the word "compact", what can I think of? Finite intersection property!

and the rest of proving (iii) was straight forward by considering the collection of closed set $f^{-1}_{\alpha}(0)$ where

$M = \bigcup_{\alpha} f_{\alpha}$


For the counterexample of when $K$ is not compact, consider the the set $C = \bigcup_{i} \\{f : \\; f(x) = 0 \\; \forall x \in (-\infty , i)\\}$ for $i = -1, -2, -3, \dots$. It is obviously an ideal, it satisfies the condition that any finite subcollection $f_1, \dots , f_r$ have common zeros, and yet they are not contained in $M_p = \\{f \in R | f(p) = 0\\}$ for any $p$.


{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}[scale=1.5, samples=100]
  \begin{axis}[
    axis lines = middle,
    xlabel = $x$,
    ylabel = {$f(x)$},
    xmin = -4, xmax = 4,
    ymin = -4, ymax = 4,
    grid = both,
    grid style = {dotted, gray!50},
    xtick = {-4,-3,...,4},
    ytick = {-4,-3,...,4},
    ticklabel style = {font=\footnotesize},
    every axis plot/.append style={thick}
  ]
  % Plot the horizontal segment (x < -1)
  \addplot [blue, domain=-4:-1, samples=2] {0};
  
  % Plot the diagonal segment (x >= -1)
  \addplot [blue, domain=-1:4] {x};
  
  % Add discontinuity indicator (open circle at jump point)
  \addplot [blue, only marks, mark=o, mark options={fill=white}] coordinates {(-1,0)};
  
  % Add filled point at (-1,-1)
  \addplot [blue, only marks, mark=*] coordinates {(-1,-1)};
  
  % Add function labels
  \node[blue, right] at (axis cs: -2.5,0.5) {$f(x) = 0$};
  \node[blue, right] at (axis cs: 1.5,1.5) {$f(x) = x$};

  \end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}



### Afterthoughts

What we have shown is that a field with a topological can be viewed as a collection of maximal ideals of a ring. (The problem used $\mathcal{R}$, but it should work for any field with a topology, since (ii) requires a field to construct the inverse but there is nothing specific to $\mathcal{R}$).

So that means an interesting connection between the structure of the maximal ideals of a ring and the topology of the field.

And note that $K$ can be ANY compact space! **Does that mean we can get different insights of the field by using different $K$?**

**And what if we want to study a subfield? Or even a subset of the field?** Will the corr. maximal ideals tell us something about it?


[^1]: Aluffi, P. (2009). Algebra: Chapter 0. American Mathematical Society. \
As a side note, Aluffi's book is really awesome as a book for brushing up algebra. Assuming you had "installed" some basic algebraic objects in your mind (i.e. know some basic group, ring, field theory), reviewing many concepts/ results through the categorical lens makes a lot of things clearer and much unified.

[^2]: From time to time when thinking about a problem it is useful to think about some related problems at once, cuz the best way to solve a problem is to understand its components well enough so that the way to the core of the problem reveals itself to you. This way you also learn more from it and are able to appreciate it more since you will get more "context" of it by thinking about its "periphery".