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

% Define the vertices of the cube Schlegel diagram
% The cube has 8 vertices, but in Schlegel diagram we see 7 (one is "inside")

% Outer square (face 1)
\coordinate (A) at (0,0);
\coordinate (B) at (2,0);
\coordinate (C) at (2,2);
\coordinate (D) at (0,2);

% Inner vertices (the "back" face projected inside)
\coordinate (E) at (0.7,0.7);
\coordinate (F) at (1.3,0.7);
\coordinate (G) at (1.3,1.3);
\coordinate (H) at (0.7,1.3);

% Draw all edges
% Outer square (face 1)
\draw[thick] (A) -- (B) -- (C) -- (D) -- cycle;

% Inner square (face 2 - the "back" face)
\draw[thick] (E) -- (F) -- (G) -- (H) -- cycle;

% Connecting edges (the other 4 faces)
\draw[thick] (A) -- (E);
\draw[thick] (B) -- (F);
\draw[thick] (C) -- (G);
\draw[thick] (D) -- (H);

% Diagonal edges to show the 3D structure
\draw[thick] (E) -- (B);
\draw[thick] (F) -- (C);
\draw[thick] (G) -- (D);
\draw[thick] (H) -- (A);

% Label vertices
\node[below left] at (A) {A};
\node[below right] at (B) {B};
\node[above right] at (C) {C};
\node[above left] at (D) {D};
\node[below left] at (E) {E};
\node[below right] at (F) {F};
\node[above right] at (G) {G};
\node[above left] at (H) {H};

% Label faces
\node at (1,1) {Face 1 (Front)};
\node at (1,0.3) {Face 2 (Bottom)};
\node at (1.7,1) {Face 3 (Right)};
\node at (1,1.7) {Face 4 (Top)};
\node at (0.3,1) {Face 5 (Left)};
\node at (1,1) {Face 6 (Back)};

% Add a legend
\node[align=left, font=\small] at (3,1) {
    Schlegel Diagram of a Cube\\
    (Regular Hexahedron)\\
    \textbf{6 faces}\\
    \textbf{8 vertices}\\
    \textbf{12 edges}
};

\end{tikzpicture}

\end{document}
```

{{< tikz >}}
\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=2]

% Define the vertices of the cube Schlegel diagram
% The cube has 8 vertices, but in Schlegel diagram we see 7 (one is "inside")

% Outer square (face 1)
\coordinate (A) at (0,0);
\coordinate (B) at (2,0);
\coordinate (C) at (2,2);
\coordinate (D) at (0,2);

% Inner vertices (the "back" face projected inside)
\coordinate (E) at (0.7,0.7);
\coordinate (F) at (1.3,0.7);
\coordinate (G) at (1.3,1.3);
\coordinate (H) at (0.7,1.3);

% Draw all edges
% Outer square (face 1)
\draw[thick] (A) -- (B) -- (C) -- (D) -- cycle;

% Inner square (face 2 - the "back" face)
\draw[thick] (E) -- (F) -- (G) -- (H) -- cycle;

% Connecting edges (the other 4 faces)
\draw[thick] (A) -- (E);
\draw[thick] (B) -- (F);
\draw[thick] (C) -- (G);
\draw[thick] (D) -- (H);

% Diagonal edges to show the 3D structure
\draw[thick] (E) -- (B);
\draw[thick] (F) -- (C);
\draw[thick] (G) -- (D);
\draw[thick] (H) -- (A);

% Label vertices
\node[below left] at (A) {A};
\node[below right] at (B) {B};
\node[above right] at (C) {C};
\node[above left] at (D) {D};
\node[below left] at (E) {E};
\node[below right] at (F) {F};
\node[above right] at (G) {G};
\node[above left] at (H) {H};

% Label faces
\node at (1,1) {Face 1 (Front)};
\node at (1,0.3) {Face 2 (Bottom)};
\node at (1.7,1) {Face 3 (Right)};
\node at (1,1.7) {Face 4 (Top)};
\node at (0.3,1) {Face 5 (Left)};
\node at (1,1) {Face 6 (Back)};

% Add a legend
\node[align=left, font=\small] at (3,1) {
    Schlegel Diagram of a Cube\\
    (Regular Hexahedron)\\
    \textbf{6 faces}\\
    \textbf{8 vertices}\\
    \textbf{12 edges}
};

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



Very weird. Perhaps it was due to 2 things:
- it was genuinely overthinking, trying to make something profound while there is actually not much things there. (e.g. trying to add more "structures" to a very very simple schlegel diagram)
- it "learned" things from the internet but it was just 鵜呑み (i.e. taking something withOUT a grain of salt. I'm not sure if there is a clean and short way to say it in english) so it added random craps into the answer.