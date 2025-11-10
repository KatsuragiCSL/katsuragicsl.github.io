---
title: "The overthinking of LLM"
math: true
tikz: true
date: 2025-11-10T17:08:21+08:00
TocOpen: true
categories: ["misc"]
tags: ['AI']
cover:
  image: "/the-overthinking-of-llm/robot-overthink.png"
---

I asked Deepseek to draw the Schlegel diagram of a hexahedron --- should be a very simple task right? Just 2 squares and link up their vertices. And yet I noticed something interesting: it tends to overthink and end up outputting nonsense answers when `DeepThink` is on (which is supposed to be more powerful and "clever"), but getting the task done correctly when `DeepThink` is off. Huh.

So this is the prompt I gave Deepseek:

> draw the schlegel diagram of hexahedron with tikz

With `DeepThink` and `Search` (accessing internet), it "thought" for >15 minutes and gave me a complete trash:

```
\documentclass{article}
\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=2]

% Define vertices for the Schlegel diagram
% Outer pentagon (face 1)
\coordinate (A) at (0,2);
\coordinate (B) at (1.9,0.6);
\coordinate (C) at (1.2,-1.6);
\coordinate (D) at (-1.2,-1.6);
\coordinate (E) at (-1.9,0.6);

% Middle ring vertices
\coordinate (F) at (0,1.2);
\coordinate (G) at (1.1,0.9);
\coordinate (H) at (1.4,-0.4);
\coordinate (I) at (0.7,-1.2);
\coordinate (J) at (-0.7,-1.2);
\coordinate (K) at (-1.4,-0.4);
\coordinate (L) at (-1.1,0.9);

% Inner pentagon (central face)
\coordinate (M) at (0,0.4);
\coordinate (N) at (0.6,0.2);
\coordinate (O) at (0.4,-0.5);
\coordinate (P) at (-0.4,-0.5);
\coordinate (Q) at (-0.6,0.2);

% Draw all edges
% Outer pentagon (face 1)
\draw[thick] (A) -- (B) -- (C) -- (D) -- (E) -- cycle;

% Connections from outer to middle ring
\draw[thick] (A) -- (F);
\draw[thick] (A) -- (L);
\draw[thick] (B) -- (F);
\draw[thick] (B) -- (G);
\draw[thick] (C) -- (H);
\draw[thick] (C) -- (I);
\draw[thick] (D) -- (I);
\draw[thick] (D) -- (J);
\draw[thick] (E) -- (J);
\draw[thick] (E) -- (K);

% Middle ring connections
\draw[thick] (F) -- (G) -- (H) -- (I) -- (J) -- (K) -- (L) -- cycle;

% Connections from middle ring to inner pentagon
\draw[thick] (F) -- (M);
\draw[thick] (F) -- (N);
\draw[thick] (G) -- (N);
\draw[thick] (G) -- (O);
\draw[thick] (H) -- (O);
\draw[thick] (H) -- (P);
\draw[thick] (I) -- (P);
\draw[thick] (I) -- (Q);
\draw[thick] (J) -- (Q);
\draw[thick] (J) -- (M);
\draw[thick] (K) -- (M);
\draw[thick] (K) -- (N);
\draw[thick] (L) -- (N);
\draw[thick] (L) -- (Q);

% Inner pentagon (central face)
\draw[thick] (M) -- (N) -- (O) -- (P) -- (Q) -- cycle;

% Draw vertices as small dots
\foreach \point in {A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q}
    \filldraw (\point) circle (1pt);

\end{tikzpicture}

\end{document}
```

{{< tikz >}}
\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=2]

% Define vertices for the Schlegel diagram
% Outer pentagon (face 1)
\coordinate (A) at (0,2);
\coordinate (B) at (1.9,0.6);
\coordinate (C) at (1.2,-1.6);
\coordinate (D) at (-1.2,-1.6);
\coordinate (E) at (-1.9,0.6);

% Middle ring vertices
\coordinate (F) at (0,1.2);
\coordinate (G) at (1.1,0.9);
\coordinate (H) at (1.4,-0.4);
\coordinate (I) at (0.7,-1.2);
\coordinate (J) at (-0.7,-1.2);
\coordinate (K) at (-1.4,-0.4);
\coordinate (L) at (-1.1,0.9);

% Inner pentagon (central face)
\coordinate (M) at (0,0.4);
\coordinate (N) at (0.6,0.2);
\coordinate (O) at (0.4,-0.5);
\coordinate (P) at (-0.4,-0.5);
\coordinate (Q) at (-0.6,0.2);

% Draw all edges
% Outer pentagon (face 1)
\draw[thick] (A) -- (B) -- (C) -- (D) -- (E) -- cycle;

% Connections from outer to middle ring
\draw[thick] (A) -- (F);
\draw[thick] (A) -- (L);
\draw[thick] (B) -- (F);
\draw[thick] (B) -- (G);
\draw[thick] (C) -- (H);
\draw[thick] (C) -- (I);
\draw[thick] (D) -- (I);
\draw[thick] (D) -- (J);
\draw[thick] (E) -- (J);
\draw[thick] (E) -- (K);

% Middle ring connections
\draw[thick] (F) -- (G) -- (H) -- (I) -- (J) -- (K) -- (L) -- cycle;

% Connections from middle ring to inner pentagon
\draw[thick] (F) -- (M);
\draw[thick] (F) -- (N);
\draw[thick] (G) -- (N);
\draw[thick] (G) -- (O);
\draw[thick] (H) -- (O);
\draw[thick] (H) -- (P);
\draw[thick] (I) -- (P);
\draw[thick] (I) -- (Q);
\draw[thick] (J) -- (Q);
\draw[thick] (J) -- (M);
\draw[thick] (K) -- (M);
\draw[thick] (K) -- (N);
\draw[thick] (L) -- (N);
\draw[thick] (L) -- (Q);

% Inner pentagon (central face)
\draw[thick] (M) -- (N) -- (O) -- (P) -- (Q) -- cycle;

% Draw vertices as small dots
\foreach \point in {A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q}
    \filldraw (\point) circle (1pt);

\end{tikzpicture}

\end{document}

{{< /tikz >}}


But without `Deepthink` and `Search`, it gave me a nice and clean (and correct!) solution:

```
\documentclass{article}
\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=1.5]

% Define vertices for the cube Schlegel diagram
% Outer square (one face of the cube)
\coordinate (A) at (0,0);
\coordinate (B) at (3,0);
\coordinate (C) at (3,3);
\coordinate (D) at (0,3);

% Inner square (the opposite face projected inside)
\coordinate (E) at (1,1);
\coordinate (F) at (2,1);
\coordinate (G) at (2,2);
\coordinate (H) at (1,2);

% Draw all edges
% Outer face
\draw[thick] (A) -- (B) -- (C) -- (D) -- cycle;

% Inner face (back face)
\draw[thick] (E) -- (F) -- (G) -- (H) -- cycle;

% Connecting edges (the other 4 faces)
\draw[thick] (A) -- (E);
\draw[thick] (B) -- (F);
\draw[thick] (C) -- (G);
\draw[thick] (D) -- (H);

% Additional edges to complete the cube structure
\draw[thick] (A) -- (B);
\draw[thick] (B) -- (C);
\draw[thick] (C) -- (D);
\draw[thick] (D) -- (A);
\draw[thick] (E) -- (F);
\draw[thick] (F) -- (G);
\draw[thick] (G) -- (H);
\draw[thick] (H) -- (E);

% Draw vertices as dots
\foreach \point in {A,B,C,D,E,F,G,H}
    \filldraw (\point) circle (2pt);

% Label vertices
\node[below left] at (A) {1};
\node[below right] at (B) {2};
\node[above right] at (C) {3};
\node[above left] at (D) {4};
\node[below left] at (E) {5};
\node[below right] at (F) {6};
\node[above right] at (G) {7};
\node[above left] at (H) {8};

\end{tikzpicture}

\end{document}
```

{{< tikz >}}

\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=1.5]

% Define vertices for the cube Schlegel diagram
% Outer square (one face of the cube)
\coordinate (A) at (0,0);
\coordinate (B) at (3,0);
\coordinate (C) at (3,3);
\coordinate (D) at (0,3);

% Inner square (the opposite face projected inside)
\coordinate (E) at (1,1);
\coordinate (F) at (2,1);
\coordinate (G) at (2,2);
\coordinate (H) at (1,2);

% Draw all edges
% Outer face
\draw[thick] (A) -- (B) -- (C) -- (D) -- cycle;

% Inner face (back face)
\draw[thick] (E) -- (F) -- (G) -- (H) -- cycle;

% Connecting edges (the other 4 faces)
\draw[thick] (A) -- (E);
\draw[thick] (B) -- (F);
\draw[thick] (C) -- (G);
\draw[thick] (D) -- (H);

% Additional edges to complete the cube structure
\draw[thick] (A) -- (B);
\draw[thick] (B) -- (C);
\draw[thick] (C) -- (D);
\draw[thick] (D) -- (A);
\draw[thick] (E) -- (F);
\draw[thick] (F) -- (G);
\draw[thick] (G) -- (H);
\draw[thick] (H) -- (E);

% Draw vertices as dots
\foreach \point in {A,B,C,D,E,F,G,H}
    \filldraw (\point) circle (2pt);

% Label vertices
\node[below left] at (A) {1};
\node[below right] at (B) {2};
\node[above right] at (C) {3};
\node[above left] at (D) {4};
\node[below left] at (E) {5};
\node[below right] at (F) {6};
\node[above right] at (G) {7};
\node[above left] at (H) {8};

\end{tikzpicture}

\end{document}

{{< /tikz >}}



Very weird.