---
title: "Playful observations with a deformation retracts and path connected-ness"
date: 2025-07-21T01:47:45+08:00
math: true
tikz: true
TocOpen: true
categories: ["mathematics"]
tags: ['topology', 'algebraic topology']
cover:
  image: "https://images.unsplash.com/photo-1738429474664-c3a0f62192f7?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
---

I was going through a problem in Lee's Topological Manifolds book[^1] (problem 7-12). It states that the infinite broom has a strong deformation retract to $(0, 0)$ but not for $(1, 0)$ (only a deformation retract). 

Below is some of my playful observations inspired by this problem. (Not restricted to the infinite broom space.)


### Inifinite Broom

{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}[scale=2.5]
    % Draw the base line [0,1]
    \draw[thick] (0,0) -- (5,0);
    \fill (5,0) circle (1pt);
    \node[below] at (0,0) {$0$};
    \node[below] at (5,0) {$1$};
    
    
    % Draw bristles for n=1 to 5
    \foreach \n in {1,2,...,5} {
        \draw (0,0) -- (5,{5/\n});
        \node[right] at (5,{5/\n}) {$\left(1, \frac{1}{\n}\right)$};
        \fill (5,{5/\n}) circle (1pt);
    }
    
    % Draw the "infinite continuation" indicator
    \draw[line width=1pt, line cap=round, dash pattern=on 0pt off 2\pgflinewidth] 
        (5,1) -- (5,0.1);

    % poor man's caption
    \node[yshift=-1cm, scale=2] at (2.5,0) {Infinite broom};

\end{tikzpicture}
\end{document}

{{< /tikz >}}


Note that the deformation retract to $(0, 0)$ itselfs imply the deformation retract to $(1, 0)$, since one can define the deformation retract to $(1, 0)$ by "first retract to $(0, 0)$, then push it to the point $(1, 0)$ along the line joining these two points".

In general:

*If a space $X$ is contractable and has a deformation retract to a point $p$, then for every point $x \in X$, X has a deformation retract to $x$*.

This can be seen by following along the idea of "first retract then push" in the infinite broom example. Note that the deformation retract to a point $p$ implies for every point $x$ there is a path joining $p$ and $x$: we can define the path $\alpha: I \to X$ by $\alpha(t) = H(x, t)$ where $H$ is the deformation retract.

So intuitively, we can say deformation retract is more "homogeneous" than strongly deformation retract, since once you can deformation retract to a point, you can do the same for every point, but the same is not true for the strongly deformation retract condition.

So what's wrong about the strongly deformation retract to $(1, 0)$ for the infinite broom?

Using our geometric intuition, the crux is the bristles "converging" to the bottom bristle (the one connecting $(0, 0)$ and $(1, 0)$). They are too close to $(1, 0)$, but there are no paths joining them with $(1, 0)$ "directly": they all have to go through $(0, 0)$, and due to continuity any deformation retract to $(1, 0)$ have to move $(1, 0)$ together with those bristles. That's why there is no strongly deformation retract to $(1, 0)$.

Formally, to prove that there is no strongly deformation retract to $(1, 0)$, it suffices to show that for every continuous function $H: X \times I \to X$ there exists a $t_0 \in I$ such that $H(t_0) \neq (1, 0)$. We can prove as the following:

Let U be an open set containing $(1, 0)$. Consider the "end" of the bristles $x_n = (1, \frac{1}{n})$. for each $n$ there is a $t_n \in I$ such that $H(x_n, t_n) \notin U$. Since $I$ is compact, there is a convergent subsequence $(t_{n_k})$ of $(t_n)$. Let $t$ be the limit. Since $(x_n)$ converges to $p$, the subsequence $(x_{n_k})$ also converges to $p$. Now by continuity $H(x_{n_k}, t_{n_k})$ converges to $H(p, t)$. However it is obvious that $H(x_{n_k}, t_{n_k})$ cannot converges to $p$ since $H(x_{n_k}, t_{n_k}) \notin U$ for all $k$.


{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}[scale=2]
    % Draw the base line [0,1]
    \draw[thick] (0,0) -- (5,0);
    \fill (5,0) circle (1pt);
    \node[below] at (0,0) {$0$};
    \node[below] at (5,0) {$1$};
    
    
    % Draw bristles for n=1 to 5
    \foreach \n in {1,2,...,5} {
        \draw (0,0) -- (5,{5/\n});
        \node[right] at (5,{5/\n}) {$\left(1, \frac{1}{\n}\right)$};
        \fill (5,{5/\n}) circle (1pt);
        % sequence converges outside
        \fill[red] (4,{4/\n}) circle (1pt);
    }
    
    % Draw the "infinite continuation" indicator
    \draw[line width=1pt, line cap=round, dash pattern=on 0pt off 2\pgflinewidth] 
        (5,1) -- (5,0.1);

    \draw[red, line width=1pt, line cap=round, dash pattern=on 0pt off 2\pgflinewidth] 
        (4,0.8) -- (4,0.1);

    % open set
    \draw[blue, dotted, line width=1mm] (4.5,-0.5) rectangle ++(1,2);


\end{tikzpicture}
\end{document}

{{< /tikz >}}

### Strongly deformation retract to a point => weakly locally path connected at that point

Another way to prove it, is by realizing our intuition "there are points too close to $p$ but can't connect to $p$ directly" is actually saying that $X$ is not locally path connected at $p$. It seems hard to prove it though, but a weaker result is straight forward:

*If a space $X$ has a strong deformation retract to $p$, then $X$ is path connected and is weakly locally path connected at $p$*.

Proof:

Path connectedness follows from the discussion about contractable space above, since a strong deformation retract is also a deformation retract.
For locally path connectedness at $p$, note that if $H: X\times I \to X$ is continuous and $H(p, t) = p$ for all $t$, then for any open set $U$ containing $p$, $H^{-1}(U)$ is an open set in $X\times I$ containing $\\{p\\} \times I$. By conpactness of $I$ there exists a open neighbourhood $V$ of $x$ such that $V \times I \subseteq H^{-1}(U)$. Note that $V$ is in $U$. Now for any $v \in V$, define $\gamma_{v}: I \to X$ by $\gamma_{v}(t) = H(v, t)$, it is obviously a path from $v$ to $p$ which lies in $U$. 

How about the (kind of) converse? If we already have a deformation retract to $p_1$, and $X$ is weakly locally path connected at $p_2 \neq p_1$, will it make a strong deformation retract to $p_2$? That looks convincing at the first glance, since from what caused the [infinite broom](#inifinite-broom) fails to have a strong deformation retract at $(1, 0)$, all we need is to make sure the sequence of points converging to $p_2$ don't move far away from it before their paths touches the line $[0,1]$, then we can retract the whole graph to $[0, 1]$ without moving $(1, 0)$


### Strongly deformation retract to p_1 + locally path connected =/=> Strongly deformation retract to another point

Counterexample: The cone of the [long line](https://en.wikipedia.org/wiki/Long_line_(topology)).

{{< tikz >}}
\usetikzlibrary{decorations.pathmorphing}
\begin{document}
\begin{tikzpicture}[scale=2.5]
    % Draw rays from cone point to base (light gray)
    \foreach \x in {-3,-2.5,...,3} {
        \draw[lightgray!90] (0,2) -- (\x,0);
    }
    
    % Draw the two boundary rays (thick black)
    \draw[thick] (0,2) -- (-3.3,0);
    \draw[thick] (0,2) -- (3.3,0);
    
    % Draw the base line with arrows and wavy segment
    \draw[thick] (-3.2,0) -- (-1,0);  % Left straight segment
    \draw[thick, decorate, decoration={
        snake, 
        amplitude=0.5mm, 
        segment length=2mm
    }] (-1,0) -- (1,0);  % Wavy segment (symbolizes long line)
    \draw[thick] (1,0) -- (3.2,0);    % Right straight segment
    \draw[thick, <-] (-3.3,0) -- (-3.2,0);  % Left arrow
    \draw[thick, ->] (3.2,0) -- (3.3,0);    % Right arrow
    
    % Label the base
    \node[below] at (0,-0.5) {Long line};
    
    % Draw and label the cone point
    \fill[black] (0,2) circle (2pt);
    \node[above] at (0,2) {};
\end{tikzpicture}
\end{document}
{{< /tikz >}}

Note that the cone of long line $CL$ has an obvious strong deformation retract to the vertex of the cone, and $CL$ is locally path connected at the bottom left corner $(0, 0)$, since $L \times \\{0\\}$ is homeomorphic to $L$ and $L$ is locally path connected (at every point), and a cone of a locally path connected space is also locally path connected. Hence $CL$ is actually not only locally path connected at $(0, 0)$ but locally path connected everywhere.

However, there is no strong deformation retract to $(0, 0)$, in fact, there is not even a deformation retract: If there is a deformation retract from $CL$ to $(0, 0)$, then the restriction to $L \times \\{0\\}$ is also a deformation retract to $(0, 0)$, but $L$ is not contractable!

Also note that the same argument applies to any points other than the vertex of the cone, hence the vertex is the only point that has a strong deformation retract to !

Each ray from $L$ to the vertex of the cone is very close to $(0, 0)$ satisfying our (wishful) heuristic argument, however it still fails to has the desired strong deformation retract. Again we see how "inhomogeneuous" strong deformation retract is, comparing to deformation retract.

Ponder a bit about how $CL$ fails, it seems like even with a good global property (the whole space is contractible) and a good locally property (locally path connected), it is still not enough to form a desired strong deformation retract. So strong deformation retract seems to be something "very global". The rays from $L$ to the vertex of cone are already closed packed, every point is locally contractible (locally it is the same as doing retraction in $[0, 1] \times [0, 1]$, which is easy), however just because there are "too many rays", it fails to have strong deformation retracts.


Next let's play a bit with shapes.


### Star shape

A well-known class of examples of contractable spaces is the star-shaped set.

A star-shaped subset $B \subseteq \mathbb{R}^n$ is a subset such that there exists a point $p \in B$ such that for every point $x \in B$ the **straight line** connecting $p$ and $x$ is also in $B$.

{{< tikz >}}
\usetikzlibrary{shapes.geometric}

\begin{document}
\begin{tikzpicture}[scale=2.5]

\node[star,star point ratio=2.25,minimum size=10cm, inner sep=0pt,draw=black,solid] {};
\fill (0,0) circle (1pt);
\node[below] at (0,0) {$p$};

\end{tikzpicture}
\end{document}

{{< /tikz >}}

Star-shaped sets obviously have deformation retract to a single point along the straight line, in particular they are also strongly deformation retracts.


### Path connected =/=> deformation retract to a point (not even to a subspace in general)

Is the condition **straight line** important? Yes, if a subspace in $\mathbb{R}^n$ satisfies the star-shaped condition but the lines joining $p$ and $x$ are not all straight lines, it can be non-contractible. Here is the classic example:


### Warsaw circle


{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16 ,
    /pgf/declare function={
            f(\x) = 1 + sqrt(\x - \x*\x);
    }
}

\begin{document}
\begin{tikzpicture}[scale=2]
  \begin{axis}[
    axis lines = middle,
    xmin = -0.1, xmax = 1.2,
    ymin = -1.2, ymax = 1.7,
    xlabel = {$x$},
    ylabel = {$y$},
    xtick = {0,1},
    ytick = {-1,0,1},
    ticklabel style = {font=\footnotesize},
    axis line style = {thick},
    clip = false,
    width = 12cm,
    height = 8cm
  ]


  % A2: Vertical segment at x=0
  \draw[blue, thick] (0,-1) -- (0,1) node[midway, left] {};
  
  % A1: Topologist's sine curve with sin(π/x)
  \addplot [blue, thick, domain=0.001:1, samples=3000] {sin(deg(pi/x))};
  \node[blue] at (0.7, -0.7) {};

  % A4: Vertical segment at x=1
  \draw[blue, thick] (1,0) -- (1,1) node[midway, right] {};
  
  % A3:  cap (1 + sqrt(x - x²))
  \addplot [red, thick, domain=0:1, samples=200] {f(x)};

  % poor man's caption
  \node[align=center, yshift=-2cm, scale=2] at (0.5, -1.0) 
    {Warsaw Circle};

  
  \end{axis}
\end{tikzpicture}

\end{document}

{{< /tikz >}}

The Warsaw circle is closed, path connected, simply connected, however is not contractable: you cannot "pull away" the sine curve from the set $\\{(0, y): -1 \leq y \leq 1\\}$.

It is also obvious that if we replace a part of the curve on top with a closed ball like skewing a fishball, the Warsaw circle still cannot retract to the ball. The problem is at the line $x=0$ where it is "very close" to something and you can't pull them apart.


### Paths is not enough to describe shapes

The above discussions shows that the fundamental group (in general, homotopy) is not a good tool to describe the shape of "ugly" topological space.

For example, the [Warsaw circle](#warsaw-circle) "looks like" a circle (and cannot be retracted) but it's fundamental group is trivial. The difficulty is that points that are close but with gaps affect the shape, but fundamental groups cannot detect this shape because there is no paths passing through the gaps.

This is the motivation of K. Borsuk's development of shape theory. But I haven't studied any of it yet.


[^1]: Lee, J. M. (2000). Introduction to Topological Manifolds (Vol. 202). Springer. ISBN: 0387987592