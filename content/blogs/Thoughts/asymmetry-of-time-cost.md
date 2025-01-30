---
draft: true
title: "Asymmetry of opportunity cost"
subtitle: "time the unequal equalizer"
math: true
tikz: true
date: 2025-01-29T00:43:14+08:00
TocOpen: true
categories: ["thoughts"]
tags: ['flaneur', 'conflicts']
cover:
  image: "https://images.unsplash.com/photo-1672093523169-f2d0b062f462?q=80&w=1964&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
---

> This is somewhat a sequel of the previous post [about the game played between the jerks and the normal people]({{< ref "/blogs/thoughts/our-legal-and-moral-system-flavors-jerks/" >}} "jump to the post"). This post also talks about some social dynamics, especially about conflicts, but not necessarily related to ethics.
> The order of sections in this post does not follow a strict waterfall model. It is not like a story telling or trying to prove some points by gradually elaborating it. It consists of a few thoughts that I had related to the same topic, hence some sections might look like standalone.

### Time is an universal equalizer, but some people have a more equal equalizer

People say "Time is an universal equalizer, everyone has exactly 24 hours a day". Indeed, everyone has equal amount of time (let's put the factor of lifespan aside), but some people's time is more equal - in the sense that, a unit of time can cost differently to different people. Let's call it the asymmetry of time cost.

Let's restrict our scope of attention so that it is clearer. We only consider the "local", but not the "global" effect of time cost here: instead of thinking about social dynamics in a long timespan like years, we look at the how the time cost asymmetry affects social dynamics at a given point in time (or over a short period of time), also we don't care about the sum of time cost of a big group of people here, but just concerns about individuals.

Let's start with a special case example: time pressure in negotiation. We all know that if you are in a negotiation and you are in a hurry to get the deal closed (perhaps your boss promised to fire you if you fail, or in an apocalyptic world you are negotiating with the only person who has the medicine to save you and your wife who are seriously ill) and your opponents knows it, they can take advantage of it.

But if we look at more general cases, as long as there are significant gap between the time costs of two players, it could be exploited. Having time pressure in negotiation is just a special case. For example in the apocalyptic world you have to get the medicine before $t=2$ or you and your wife die. In contrast, it is not urgent for the person who posesses the medicine to get what you can offer him/ her. In this case the time costs will be something like this:

{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}[scale=1.5, samples=100]
\begin{axis}[grid=both,
          xmax=pi,ymax=10,
          axis lines=middle,
          restrict y to domain=-7:12,
          enlargelimits]

\addplot[blue,domain=0:2]  {1/(2-x)-1/2};
\node[text=blue] at (1.5,8.2) {you};
\addplot[red,domain=0:4]  {x/4};
\node[text=red] at (3,2.2) {opponent};
% filling scope
% fk this shit i cannot use fillbetween
\begin{scope}
  \clip (0,0) -- plot[smooth,samples=200,domain=0:2](\x,{1/(2-\x)-1/2}) -- (2,0);
  \clip (0,0) -- plot[domain=0:2](\x,{\x/4}) -- (2,12);
  \fill[gray,opacity=.3] (0,0) rectangle (2,12);
\end{scope}
\end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}

Your curve raises rapidly since the longer the negotiation takes, the more risky is your lives. It does not have values at and beyond time $t=2$, since you would already be dead. For your opponent, since he/ she is not in rush, say, he/ she only wants your food but is not starving[^1], so as time passes he/ she gets hungrier, but it does not make much difference.

If we assume, as time passes the other aspects of the negotiation remain the same, then the gray area between those curves will be the extra profit he can gain from you.

In general, you don't have to be in a life-or-death situation, only a small gap bewteen your time cost between someone else's is enough for a potential abuse. One hilarious example: when you are arguing with a guy outside in a hot summer, the guy has got cold drink in his hand while you don't... the time cost curves could be just something like this. Not a big difference, but enough for you to try to get it done as soon as possible:

{{< tikz >}}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}[scale=1.5, samples=100]
\begin{axis}[grid=both,
          xmax=10,ymax=10,
          axis lines=middle,
          title style={at={(0.5,0)},,anchor=north,yshift=-10},
          title=irconically the one without a cold drink should be the one in red color,
          enlargelimits]

\addplot[blue,domain=0:10] {1.3*x};
\node[text=blue] at (2,7) {without a cold drink};
\addplot[red,domain=0:10]  {x};
\node[text=red] at (4,1) {with a cold drink};
% filling scope
% fk this shit i cannot use fillbetween
\begin{scope}
  \clip (0,0) -- plot[smooth,samples=200,domain=0:10](\x,{1.3*\x}) -- (10,0);
  \clip (0,0) -- plot[domain=0:10](\x,{\x}) -- (10,30);
  \fill[gray,opacity=.3] (0,0) rectangle (10,30);
\end{scope}
\end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}

Note that the same person can have a quite different time cost curve in different periods of time: to a busy 9-5 worker, his time on weekdays might be more precious than on weekends. Even within the same day, the time when the worker is heading home from work, got off the train and walking to his/ her place from the train station, could cost him/ her almost zero. The time when he/ she is heading to the office in the morning while being already a little bit late, costs totally differently.

One more thing to note: time cost is not necessarily the same as opportunity cost. Opportunity cost is what you lose because you don't choose to do something else which you could have use the time to do, but in some cases you don't have other choices, so it does not make sense to talk about opportunity costs. In some cases, it could be think of as time value of futures: the closer it gets to the delivery date, the less risk it is to someone who is going to profit because from it. Opportunity cost comes from the alternatives available in a given timespan, time cost can come from opportunity cost, but it can also come the passing of time itself.

I would say time cost = opportunity cost + "other factors", but I cannot exhaust what that "other factors" could be. They are most likely something cannot control. It could be risk, could be some known cost (as opposed to risk) induced from the time lapse (imagine you have a leaking pipe), it could be some known cost (as opposed to risk) induced from the remaining time until the occurance of a given event (as opposed to risk which you may or may not know when will the unfavorable event comes, if it happens). See some of the examples below.


### Low time cost != poor

Sometimes people mistake time cost as "what you can lose" and they think the lower social status someone has the less time costs him/ her. But it's not true. Indeed poverty/ low social status could cause lower time cost, but not always, and in contrast a person has lower time cost does not imply that he is poorer.

In daily life, there are a few examples of people with relatively low time cost who are not poor:
1. Old people
2. Owners of stable business (in contrast to, say, small business, or quickly expanding/shrinking businesses, in which the owner has many things to take care of)
3. 9-5 workers in a gov job (when at work)
4. People who work in an industry in which their impact is not consistently highly related to the time they put in (when at work)

**Old people:**

The case of old people is really ironic. They have very little time left in their lives, comparing to young people, so one should expect every minute is important to them right? And yet a lot of old people act like time is of zero or even negative cost so they have to find ways to kill time, like sitting in a park and chatting random nonsense all day long, almost like doing nothing. It is because they have nothing they want or need to do, hence they don't need the time for those things.

**Owners of stable business:**

Small business or unstable bussiness can eat up a huge portion of their owner's time. But a stable one, well, the owners can almost do nothing but count his money. Since they are financially secure without much time input, they can have a relatively laid back life if they want. But in case you were an ambitious owner of a gigantic corp and had tons of thing to achieve, like Elon Musk[^2], that would not be the case. So it is not totally about wealth.

**9-5 gov job workers:**

a good amount of 9-5 gov job workers are just walking deads (at work). They can even intentively entend the time needed for a given task. When you have to pretend that you have a lot of important things to do while you actually don't, the closer it gets to 5pm the less struggle you have to bare for looking ways to pretend having work.

**People who work in an industry in which their impact is not highly related to the time they put in:**

In some industry, the impact of your work highly related to the amount of time you put in, for example average small bakery workers: unless you are a bakery artist who sells unique breads, the process of bakery is extremely standardized and the number of breads you make is at a almost fixed ratio to the time you spend on making the dough. If you spend less time in making the dough and you make one dough less today, you sell one bread less.

But creative workers are differently, let's say song writers. Except at the last step when you actually write down the song (on papers or digitally), putting one more hour on trying to come up a new song at any given moment does not have much to do with how good the song will be. In fact going for a walk or even put it aside for months might actually help.

Of cause the more you think about it, the more likely it is going to be good, or at least in the long run you will be better at writing songs, but since you cannot predict how useful is your effort in the next hour or even the next week, if your friends interrupt your work and take you out for drinking, you won't hesitate too much, comparing to a bakery worker's friend ask him out for drinks at 4am *(huh?)* when he is making the dough...

![](/asymmetry-of-time-cost/have-to-work.jpeg)


### People exploit time cost differentials without knowing (or do they?)

The exploitation of time needs not to be intentional: The simplest example is when a bunch of idler slowly walking in a row on the street and blocking others who are relatively in a hurry (or who just naturally walks faster, since the longer you walking unnaturally slow the more uncomfortable you get). They might not be intended, but they do annoy others.

![](https://media.istockphoto.com/id/1035560708/zh/%E7%85%A7%E7%89%87/%E5%B9%B4%E8%BC%95%E4%BA%BA%E5%9C%A8%E8%A1%97%E4%B8%8A%E6%95%A3%E6%AD%A5.jpg?s=1024x1024&w=is&k=20&c=eJuXBVjhvo2DePUUmIHy-pPvaBZko7rYuvcsEg5Y0bQ=)

Another example: Hotel staffs in some countries are notorious for being super slow. It could be pretty normal in their standards because of cultural or economical differences, but visitors from countries who are used to fast paces will often get annoyed.

Yet another example: imagine in the workplace in the same team, there is a close-to-retire old man who does not care about work much, completely OK with delays; and another young lad who wants to have a good career and at least finish stuff on time. If most of the tasks need both of them working together to get done, this team will be a disaster. 

Yet yet another example: imagine a man whose working hours is the complete opposite of the majority. He works when most people rest, and he can only enjoy his free time in peak hours, which gets him annoyed by the crowd and the impatience he gets everywhere, when he just wants to relax. 

Yet yet yet another example: travellers at popular places v.s. local people who live nearby.


### Will all the problems be solved if we don't allow people with different time costs interact?

Okay, this might be an insane thing say it out loud, but bare with me. If exploits happens everyday between people with high time cost and people with low time cost, how about we segregate them? Like what people used to do with races just because they think some races are more precious?(**DISCLAIMER: racial segregation is wrong and the author does NOT support it**) In that case people will almost only interact with other peopl who have roughly the same time cost curve as they have, there will be no more exploits. Let's assume there is a costless way to implement it, will it solve our problems, or create another problems (except ethical ones)?

I don't know for sure, but I think the answer is no. One interesting implication I can think of: very likely no one will be the security guard of the apartment building you live in. Security guards in apartment buildings are one of the groups that have very low time cost: the majority of their work is just let the time pass. They won't bother if any ad hoc thing jumps in to consume their time. That's why some bad security guards spite visitors, sometimes they also spite those who live there as well. So unless the whole building are full of people live like a security guard, otherwise you won't get a security guard of your building.

It probably just sucks.


[^1]: If he or she is in fact starving, very close to death or any circumstances that would be a deal breaker (for example he/ she faints - in that case you might be able to just rob him/ her and he/ she will get nothing), his/ her curve will look pretty much the same as yours. In fact, in such case both side should almost immediately come to concensus: just swap the food and medicine so that both side can be saved.
[^2]: Elon Musk said he works [70-120 hours work per week](https://www.youtube.com/watch?v=Ku6c2rJG35g). I doubt it though, especially after he [mastered Diablo 4](https://www.forbes.com/sites/paultassi/2024/11/22/elon-musk-apparently-just-became-the-no-1-diablo-4-player-in-the-world/). Unless he cheated or lied on one of his claims, or both. 