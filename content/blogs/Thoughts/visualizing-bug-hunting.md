---
title: "Visualizing Attack Surface Mapping"
date: 2024-06-24T01:16:11+08:00
draft: true
TocOpen: true
categories: ["thoughts"]
tags: ['methodology']
---

## Introduction

I was auditing a system that was designed to be managing users but in the anonymous way - The system assign an object to a user, which is unique to the user, but the system MUST NOT be able to correlate a particular user with the object associated with him/ her.

That sounds confusing, let's imagine the following use case:

__XV DIP to be filled here__

When I was trying understand why the whole design works and visualize it, I found that my visualization can be applied to general bug hunting (or more precisely, attack surface mapping) process, giving me a clearer understanding of "what am I doing" and "is there anything I missed", instead of just brainstorming in the dark and HOPE that I have covered enough attack surface.

Before going to the visualization of this design, let's look at a more trivial example first:

## Attack as adding edges

*Man muss immer mit den einfachsten Beispielen anfangen.*[^1] - Here is a simple example: a typical bank system API, allowing user to retrive their account balance, and allowing customer supports to retrieve personal information such as client's names, phone numbers, residental addresses etc. We put aside the "write" functionality such as deposition/ withdrawal first for simplicity, consider only the "read" functionalities as above. Let's sketch a graph to represent it

![](/visualize-attack/visualize-attack-1.png)

The graph above showing the "normal" flow of this system.
Objects in circles are **data**, they cannot take actions, cannot receive data (this sentence sounds odd though). They can only be accessed.
Objects in rectangles are **agents**, they can receive data and/ or perform actions, such as sending data, 

With this graph, to brainstorm an attack case can be done by attempting to draw an unexpected edge: 
- what if I can draw a line from user 1 to user 2 data? -> classical IDOR
- what if I can draw a line from any user to the api server/ data(database) without going through cloudflare? -> bypassing cloudflare due to misconfigs.
- what if I can draw a line from user 1 to CS/ devs (so that at the end the path reaches any user data) -> compromising CS/ devs and gain access to data



Now I am sharing my graph for the __XV_DIP__ for fun:

__GRAPH__

[^1]: "One must always begin with the simplest examples.", usually attributed as a quote from David Hilbert, although I cannot find a firm source.