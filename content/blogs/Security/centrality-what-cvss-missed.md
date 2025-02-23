---
title: "Centrality: how we actually perceive the severity of a bug"
subtitle: "...and the deficiency of the CVSS scoring and other such quantification systems"
math: true
tikz: true
date: 2025-02-23T02:59:19+08:00
TocOpen: true
categories: ["security"]
tags: ['philosophy']
cover:
  image: https://images.unsplash.com/photo-1664526936810-ec0856d31b92?q=80&w=1932&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
---

### An empty business lingo or a good quantification?

We hope to, and probably need to, quantify the severity of security bugs. The “need” mainly comes from the fact that we have to provide an interface to management: We need to have a reasonably objective quantification to tell how serious an issue is (and show that we would not overplay/downplay something for our own self-interest), and that would lay the groundwork for the establishment of a bug handling standard that the engineering team would follow.

But do our quantifications accurately reflect the severity of the bugs? Or do they reduce themselves to merely buzzwords and props for business talks?

Business lingo usually does not match the aesthetics of technical people: sometimes they are even allergic to the vocabulary of business talk so much that they want to escape from it, like Nero in the traders' story in *Fooled by randomness*[^1] (except when they have to boast or to look for jobs on LinkedIn, of course, since after all we have to feed ourselves right? :smirk:). So when something annoys technical people and they complain about the technical inaccuracy, most of the time it is because the thing contains a bit too much business lingo.

As the CVSS scoring system[^2] evolves over these years, it becomes more and more complicated, and yet still addressing the severity of bugs in a not very ideal way. I and my colleagues have ranted about it, `curl`’s author also [complained](https://daniel.haxx.se/blog/2025/01/23/cvss-is-dead-to-us/) about it - I believe there are more people out there who are not happy with it.

We also have the P-level system: like the one of [Bugcrowd](https://bugcrowd.com/vulnerability-rating-taxonomy) which divides the severity of bugs into 5 levels, according to the bug types. This system gives us more flexibility on some occasions, especially when the severity is “varies” in the taxonomy. But that does not make things clearer, it just sweeps the messy part of the problem under the carpet: instead of stating what is it that determines the actual severity in such cases, it leaves the judgment to the free evaluation of a blackbox (the one who makes the final decision) and trusts the outcome. \
To be fair, usually it is not a serious problem to those who have solid experience in dealing with vast varieties of security bugs, but in this case, instead of accusing it of being an inaccurate/ambiguous scale, I will try to **expose the hidden concept** we used when we are making such decisions, which is the main goal of this article.


### Not all P5 are equal

Let’s start with an imaginary yet realistic example:

Consider two bugs. Bug 1 is a “Missing ‘HttpOnly’ Cookie Attribute”. Bug 2 is a theoretical cryptographical weakness in the signing algorithm used in a JWT (which is in the cookie and is used for authenticating users).

I am pretty sure both will get a very low score in the CVSS system or a P5/informational in Bugcrowd’s vulnerability rating. But after marking the scores/ P-level for them, how strongly do you feel that we should fix these issues? Although both of them are not serious problems, I feel a much stronger urge to fix bug 2, and I believe many people would feel the same way. But why do we feel this way?

The naive approach to explain it is with the ratio of “hardness to exploit” to “impact”. But that’s actually the high level approach of CVSS, CVSS already broke it down for you: attack complexity, user interaction, privilege required, etc. are just a breakdown of “hardness to exploit”, and the CIA scoring is the breakdown of “impact”. Both bug 1 and bug 2 have almost zero exploitability and very similar impact. That’s exactly why the CVSS framework cannot explain the distinction.

However, if we introspect we will find that the perceived severity is affected by whether the issue is the “real meat” or not:
Missing HTTPOnly cookie attribute could surely lead to cookie stealing, but it is like the last straw on the camel’s back, it’s peripheral, boring, not important, and far away from being one of the “key steps” in stealing cookies. In contrast, the signing algorithm is the bread and butter of JWT, it is a crucial part.

But how do we articulate that?


### Centrality

I first learned the concept of centrality from Timothy Gowers's talk on 2022 Fields Medal Symposium[^3]. He used centrality (as one of the factors) to explain why we consider some problems to be more “interesting” than others. I found that this concept can be applied in similar ways to explain several things out of the mathematical realm, including how we perceive the severity of a bug.

In short, the more centrality a bug has, the more important and fix-worthy it is.

If you plot out all the attack/defense mechanisms and other components related to the component in concern, the more important a component is, the more connections with other things in the graph it will have. They will look more “central” in the graph.

If you plot such a graph for the cryptography of the JWT you will see multiple attack techniques linked to it: changing the algo, breaking the encryption, abusing symmetric encryption, etc. \
But the httponly cookie attribute is sitting humbly at the border with just one connection: “given XSS exists, retrieve the cookie” (there could be more, but in any case, it is way less than that of the JWT), and if we consider the bigger picture of XSS, most of the connections happen at the node that represents the data that got inserted into js.

Imagine you need to flow some water from the sources to the end like in the graph below:

{{< tikz >}}
\usepackage{tikz}
\usepackage{tikz-cd}
\tikzcdset{scale cd/.style={every label/.append style={scale=#1},
    cells={nodes={scale=#1}}}}
\begin{document}
  \begin{tikzcd}[scale cd=2]
    \node[circle,fill=black] at (360:0mm) (center) {};
    \foreach \n in {1,...,5}{
        \node[circle,fill=black] at ({\n*360/5}:4cm) (n\n) {};
        \draw[<-][blue,line width=1mm] (center)--(n\n);
        \node[right=2pt] at ({\n*360/5}:4cm) (n\n) {source};
    }
    \node[circle,fill=black] at (-7,0) (outer) {};
    \draw[<-][blue,line width=1mm] (outer)--(center);
    \node[circle,fill=black] at (-10,0) (end) {};
    \draw[<-][blue,line width=1mm] (end)--(outer);
    \draw[->][blue,line width=1mm] (center) to[out=-160,in=-70] (outer);
    \draw[->][blue,line width=1mm] (center) to[out=160,in=70] (outer);

    \node[above=4pt] at (-10,0) {end};
  \end{tikzcd}
\end{document}
{{< /tikz >}}

Which situation triggers you more? Is it when the “center” node has a minor dysfunctioning:

{{< tikz >}}
\usepackage{tikz}
\usepackage{tikz-cd}
\tikzcdset{scale cd/.style={every label/.append style={scale=#1},
    cells={nodes={scale=#1}}}}
\begin{document}
  \begin{tikzcd}[scale cd=2]
    \node[circle,fill=red] at (360:0mm) (center) {};
    \foreach \n in {1,...,5}{
        \node[circle,fill=black] at ({\n*360/5}:4cm) (n\n) {};
        \draw[<-][blue,line width=1mm] (center)--(n\n);
        \node[right=2pt] at ({\n*360/5}:4cm) (n\n) {source};
    }
    \node[circle,fill=black] at (-7,0) (outer) {};
    \draw[<-][blue,line width=1mm] (outer)--(center);
    \node[circle,fill=black] at (-10,0) (end) {};
    \draw[<-][blue,line width=1mm] (end)--(outer);
    \draw[->][blue,line width=1mm] (center) to[out=-160,in=-70] (outer);
    \draw[->][blue,line width=1mm] (center) to[out=160,in=70] (outer);

    \node[above=4pt] at (-10,0) {end};
  \end{tikzcd}
\end{document}
{{< /tikz >}}

...or when the end node has a minor dysfunction?

{{< tikz >}}
\usepackage{tikz}
\usepackage{tikz-cd}
\tikzcdset{scale cd/.style={every label/.append style={scale=#1},
    cells={nodes={scale=#1}}}}
\begin{document}
  \begin{tikzcd}[scale cd=2]
    \node[circle,fill=black] at (360:0mm) (center) {};
    \foreach \n in {1,...,5}{
        \node[circle,fill=black] at ({\n*360/5}:4cm) (n\n) {};
        \draw[<-][blue,line width=1mm] (center)--(n\n);
        \node[right=2pt] at ({\n*360/5}:4cm) (n\n) {source};
    }
    \node[circle,fill=black] at (-7,0) (outer) {};
    \draw[<-][blue,line width=1mm] (outer)--(center);
    \node[circle,fill=red] at (-10,0) (end) {};
    \draw[<-][blue,line width=1mm] (end)--(outer);
    \draw[->][blue,line width=1mm] (center) to[out=-160,in=-70] (outer);
    \draw[->][blue,line width=1mm] (center) to[out=160,in=70] (outer);

    \node[above=4pt] at (-10,0) {end};
  \end{tikzcd}
\end{document}
{{< /tikz >}}


In the case of the dysfunctioning worsening/getting “exploited”, both case stops water flow from the source to the ends, but the center node case just looks more critical. Even if we assume the cost of fixing the issue is the same in both cases (say we can just click a button and a new node for replacing will be spawned like magic).

Is that feeling an illusion, i.e. none of the above situations is worse than another? I believe not:

More connections mean more uncertainty in evaluation: maybe we missed something even though our investigation says it is all fine.

More connections also mean more hidden implications, a currently harmless issue (sometimes we describe as “weridness”, “not the best practice”) may be already quitely changing the behaviors of other things that are related, and those changes might chain up and cause some other weirdness.

More connections also mean the experience we gain by looking into it is possibly more useful in the future.


[^1]: Taleb, Nassim Nicholas, 1960-. (2001). Fooled by randomness : the hidden role of chance in the markets and in life. Penguin Books.
[^2]: At the time of writing, the latest version is CVSS 4.0: https://www.first.org/cvss/v4-0/. I, as a security worker, find it a bit painful to use as well.
[^3]: https://www.youtube.com/watch?v=EcdW3i6psmI 