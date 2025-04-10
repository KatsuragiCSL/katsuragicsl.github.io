---
title: "A more intuitive explanation of Burnside's lemma"
math: true
tikz: true
date: 2025-04-10T00:56:29+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['algebra', 'intuition', 'visual']
cover:
  image: "https://images.unsplash.com/photo-1488229297570-58520851e868?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8SW50dWl0aW9ufGVufDB8fDB8fHwy"
---

{{< notice warning >}}
You need to know some basic group theory terminology to appreciate(I hope you do) the following content.
{{< /notice >}}

### Burnside's lemma

Here is the statement of the Burnside's lemma:

Let $G$ be a group that actions on a set $X$. Denote $X^{g}$ the set of fixed points of $g$ i.e. $\\{x \in X | g \cdot x = x\\}$, then the number of orbits of the action is equal to $\dfrac{1}{|G|}\sum\limits_{g \in G} |X^g|$.

### Let's persuade ourselves that this is true first

Instead of rushing to an attempt to prove, let's try to persuade ourselves that this is true first.

If we think of the action of $G$ on $X$ as like stirring the soup and try to mix the ingredient evenly, then the more orbits you have, the less evenly you mixed it (of cause inside the orbit it could be well mixed, but imagine the extreme case when there are too many orbits so all orbits are small).

How about the formula $\dfrac{1}{|G|}\sum\limits_{g \in G} |X^g|$ ? Since it is a sum divided by $|G|$, we can think of it as the average of something. What is that "something"? Fix a $g \in G$, imagine an $x \in X$ is a particle in the soup, then $x \in X^g$ means $g$ did not move $x$, so your stirring did not really stir $x$ at all! The larger $X^g$ you have, the more particles you did not move, hence the less evenly you mix the soup. So what the lemma say is, roughly: 

> How unevenly you stir your soup is the average number of particles you did not move for one stroke of stirring.

Sounds pretty legit!

![](https://images.unsplash.com/photo-1624893464449-22a7e40de7c9?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MjR8fHN0aXJyaW5nfGVufDB8fDB8fHwy)

### High level plan of attack

How can we prove this lemma? Let's contemplate the concepts involved in the statement, see what the gap is, explore what related concepts are in the gap.

What we have:
- the size of the set of what a given $g$ does not move
- the size of $G$ i.e. the number of $g$
- the number of orbits

What we want: a good relation between them(more precisely, an equality as the lemma stated).

Well, since the size of each orbits can be all different, and they can be quite arbitrary, we may eventually need a way relates the sizes of orbits with some of the quantities above, otherwise the **number** of orbits can't seem to bridge to the **sizes** of things.

Now, since counting orbits is counting things in $X$, you might want to think about some "good" set of $g$ for a fixed $x$. Since we are already considering a set of $x$ that a given $g$ does not move, maybe it is good to consider a set of $g$ that a given $x$ does not move - That's how we can come up with the concept of stabilizer.

If you already know Orbit-Stabilizer theorem you would have very likely thought of it since the concepts look so closely related. But even if you don't, it is still likely that you can figure out that you need Orbit-Stabilizer theorem (and figure out its proof by yourself as well) with the above motivation. I am also going to give a intuitive explanation of Orbit-Stabilizer theorem below (I keep it short since it is mostly the same as how everyone think of it when they learnt it the first time).

So in summary here is 3 thing we need:
1. Connect the number of orbits with some sizes
2. Orbit-Stabilizer theorem
3. Counting $\sum\limits_{g \in G} |X^g|$ in a different way


### Connect the number of orbits with some sizes

How can we deal with the annoyingly arbitrary sizes of orbits? When we have trouble in unifying things with different sizes, the first thing to try is to **normalize** things by dividing by their sizes (think about normal vectors and how we construct orthonormal basis in linear algebra).

With this idea, it is not hard to see that $\sum\limits_{x \in X} \dfrac{1}{|\mathcal{O}_x|} =$ number of orbits, where $\mathcal{O}_x$ is the orbit of $x$. This is well defined since orbits are disjoint.

One "free" observation: Since we already considering the sizes of orbits, it is natural to see that the sum of sizes of all the orbits is equal to the size of $G$.

### Orbit-Stabilizer theorem

Fix a $x \in X$, then the size of the orbit of $x$ multiplied by the size of the stabilizer is equal to $|G|$.

Intuitive explanation: think about $G$ "modding out" what does not move $x$. 


### Different ways to count edges

Here come the next part: how to count $\sum\limits_{g \in G} |X^g|$ ?
Let's draw a bipartite graph such that $x$ connects with $g$ when $g \cdot x = x$. For instance:

{{< tikz >}}

\usepackage{tikz}
\usetikzlibrary{positioning,chains,fit,shapes,calc}

\begin{document}

\definecolor{myblue}{RGB}{80,80,160}
\definecolor{mygreen}{RGB}{80,160,80}

\begin{tikzpicture}[thick,
  every node/.style={draw,circle},
  fsnode/.style={fill=myblue},
  ssnode/.style={fill=mygreen},
  every fit/.style={ellipse,draw,inner sep=-2pt,text width=2cm},
]

% the vertices of X
\begin{scope}[start chain=going below,node distance=7mm]
\foreach \i in {1,2,...,6}
  \node[fsnode,on chain] (f\i) [label=left: $x_{\i}$] {};
\end{scope}

% the vertices of G
\begin{scope}[xshift=4cm,yshift=-0.5cm,start chain=going below,node distance=20mm]
\foreach \i in {1,2,3}
  \node[ssnode,on chain] (s\i) [label=right: $g_{\i}$] {};
\end{scope}

% the set X
\node [myblue,fit=(f1) (f6),label=above:$X$] {};
% the set G
\node [mygreen,fit=(s1) (s3),label=above:$G$] {};

% the edges
\draw (f1) -- (s1);
\draw (f1) -- (s2);
\draw (f2) -- (s1);
\draw (f3) -- (s1);

\draw (f4) -- (s2);
\draw (f5) -- (s2);

\draw (f6) -- (s3);

\end{tikzpicture}
\end{document}

{{< /tikz >}}

Now, what is $\sum\limits_{g \in G} |X^g|$? - we pick $g$ one at a time, look at how many $x$ is connected with it, finally add up those numbers.

This is the same as counting the number of edges in the graph.

So what is another way to count the number of edges in the graph? - we can also pick $x$ one at a time, look at how many $g$ is connected with it, finally add up those numbers. And notice that for a given $x$, the number of $g$ connected with it is just the size of the stabilizer: $|G_x|$.

Hence, we can see that $\sum\limits_{g \in G} |X^g| = \sum\limits_{x \in X} |G_x|$.

Combine what we have, now it is obvious why Burnside's lemma is true: the number of orbits is just the sum of $\dfrac{1}{|\mathcal{O}\_x|}$ over all $x$, which is $\dfrac{1}{|G|}\sum\limits_{x \in X} |G^x|$ (by Orbit-Stabilizer theorem), which is $\dfrac{1}{|G|}\sum\limits_{g \in G} |X^g|$.


### Epilogue

The first remark is that the above is not a rigorous proof, since we assumed $G$ and $X$ to be finite for the sake of intuitive explanation.

The second remark: After I figured out the proof by myself, I went to google if there are any intuitive explanation online. Seems that none of the articles/discussions I found (the first-few-ish search results) provide a explanation with intuitive AND ELEMENTARY flavour. Although some people did give explanation with "higer level" math, such as Tao[^1].

[^1]: https://mathoverflow.net/questions/50033/intuitive-explanation-of-burnsides-lemma