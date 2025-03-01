---
title: "[Updated 20250301]Centrality: how we actually perceive the severity of a bug"
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

{{< notice info >}}
**Updates**:\
After giving a second thought on the topic and reorganizing the materials, I had a sharing session with my teammates and decided to update this article accordingly. Updates include more suitable examples and graphics.
{{< /notice >}}

### An empty business lingo or a good quantification?

We hope to, and probably need to, quantify the severity of security bugs. The “need” mainly comes from the fact that we have to provide an interface to management: We need to have a reasonably objective quantification to tell how serious an issue is (and show that we would not overplay/downplay something for our own self-interest), and that would lay the groundwork for the establishment of a bug handling standard that the engineering team would follow.

But do our quantifications accurately reflect the severity of the bugs? Or do they reduce themselves to merely buzzwords and props for business talks?

Business lingo usually does not match the aesthetics of technical people: sometimes they are even allergic to the vocabulary of business talk so much that they want to escape from it, like Nero in the traders' story in *Fooled by randomness*[^1] (except when they have to boast or to look for jobs on LinkedIn, of course, since after all we have to feed ourselves right? :smirk:). So when something annoys technical people and they complain about the technical inaccuracy, most of the time it is because the thing contains a bit too much business lingo.

As the CVSS scoring system[^2] evolves over these years, it becomes more and more complicated, and yet still addressing the severity of bugs in a not very ideal way. I and my colleagues have ranted about it, `curl`’s author also [complained](https://daniel.haxx.se/blog/2025/01/23/cvss-is-dead-to-us/) about it - I believe there are more people out there who are not happy with it.

We also have the P-level system: like the one of [Bugcrowd](https://bugcrowd.com/vulnerability-rating-taxonomy) which divides the severity of bugs into 5 levels, according to the bug types. This system gives us more flexibility on some occasions, especially when the severity is “varies” in the taxonomy. But that does not make things clearer, it just sweeps the messy part of the problem under the carpet: instead of stating what is it that determines the actual severity in such cases, it leaves the judgment to the free evaluation of a blackbox (the one who makes the final decision) and trusts the outcome. \
To be fair, usually it is not a serious problem to those who have solid experience in dealing with vast varieties of security bugs, but in this case, instead of accusing it of being an inaccurate/ambiguous scale, I will try to **expose the hidden concept** we used when we are making such decisions, which is the main goal of this article.


### Not all P5 are equal

Let’s start with an imaginary yet realistic example:

Consider two bugs. \
Bug 1 is a “Missing Secure Cookie Attribute”. \
Bug 2 is a Weird input reflection: the input in a `GET` parameter is splitted into 2 parts and reflected into 2 different places in the same page, but no one could find a valid XSS, and sanitization is in place.

Now bug 1 is a standard low severity issue, in fact, in practice it is quite often to be treated as informational. For bug 2, it falls under the category of a standard informational issue (user input reflection) although its behavior is not quite standard among the issues in that category. 

So in reality they will both be treated as with roughly the same severity, the input reflection one will probably be lower.

However, if you could only fix one of them, which one would you choose? (In reality you could choose "both", but let's pretend, for the sake of thought experiments).

I would choose the input reflection one. Let's do some analysis. The core idea of CVSS and the usual practice of how people evalute severity today can be summarized as calculating the ratio of "how hard/likely to exploit" to "how bad is the impact". Let's see the comparison on "how hard/likely to exploit":

| Cookie without secure flag             | Input reflection    |
|:---------------------------------------|:--------------------|
| Need to have the target website allow HTTP   | Need a way to bypass sanitization                                 |
| Need to trick the user to click on HTTP link | Need a way to trigger the payload correctly after the input split |
| Need MITM to capture the cookie              | Need user to click the link for the reflected XSS                 |

For the impact part:

| Cookie without secure flag             | Input reflection    |
|:---------------------------------------|:--------------------|
| Stealing the cookie (you get the MITM) | Stealing the cookie |
| Leaking the cookie to whoever has MITM | Further phishing    |

You would probably agree that their "how hard/likely to exploit" to "how bad is the impact" ratio look quite close.

However, if you break down how exactly are they being "unlikely to happen/hard to exploit", you will have a different point of view. We can do so by asking questions like "how do they fit in to a bigger picture?", "how can I manipulate it in a different way?". So here is another table:

| Cookie without secure flag             | Input reflection    |
|:---------------------------------------|:--------------------|
| Only relevant to cleartext transmission issue between the user and the web server Not linked to many different things | There might be a way to trigger the input split in an useful way                                                                        |
|   | The sanitization library might have bugs  |
|   | If there are subdomains that gets data from the site which has the reflection issue, and they do some "weird" manipulation to the data...   |

There are way more ways to play with the input reflection issue, it is connected with more things.

The “use cases” of the reflection issue is all extremely hypothetical. But they cast more shades over our analysis: it feels like there is a black swan in one of the corners in the world, you just know it is unlikely to be the next corner you are going to turn.

Meanwhile, dealing with the Cookie Secure flag issue is (almost) like walking on a straight road. You see a fierce dog in front of you which look like going to bite you if you come close. Well Ok, I can just stop walking. Nothing scaring hiding in shadow.

But how do we articulate the analysis above? What is the concept behind it?


### Centrality

I first learned the concept of centrality from Timothy Gowers's talk on 2022 Fields Medal Symposium[^3]. He used centrality (as one of the factors) to explain why we consider some problems to be more “interesting” than others. I found that this concept can be applied in similar ways to explain several things out of the mathematical realm, including how we perceive the severity of a bug.

If you plot out all the "connections", the more connections a thing have, the more they will look more “central” in the graph:

![](/centrality/centrality.png)

A more abstract example:

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


In the case of the dysfunctioning worsening/getting “exploited”, both case stops water flow from the source to the ends, but the center node case just looks more critical. Even if we assume the cost of fixing the issue is the same in both cases (say we can just click a button and a new node for replacing will be spawned like magic). But you probably feel more urge to look at the center node as it looks like there are more things you could dig into.

Centrality causes a few things: 

- Bring uncertainty into play
- Hidden implications
- More flexibility (hence more likely to have some new ways to break known defenses)

Also...although it does not affect the severity, but it does courage us to pay more attention on things that have more centrality: more transferable lessons you will learn from dealing with it.

Hence, centrality is definitely one of the factors for evaluating the severity of a bug, the more centrality the more severe. However it is missed in the current quantification systems and not even mentioned by people although they might be using it in a daily basis.

[^1]: Taleb, Nassim Nicholas, 1960-. (2001). Fooled by randomness : the hidden role of chance in the markets and in life. Penguin Books.
[^2]: At the time of writing, the latest version is CVSS 4.0: https://www.first.org/cvss/v4-0/. I, as a security worker, find it a bit painful to use as well.
[^3]: https://www.youtube.com/watch?v=EcdW3i6psmI 