---
layout: post
title: "A Pragmatic Exploration of Tech Debt"
date: 2012-03-03 12:14
comments: true
published: false
categories: 
---

###TODO: Amortization Plan
This post explores the concept of tech debt.  In particular I would like to disect the jumbled notion of tech debt and discuss each discreet concept in detail.  In some ways you can think of this essay as a refactoring of the idea of tech debt.  I am striving to approach tech debt from a scientific and pragmatic point of view.  I plan to explain each step of this exploration so as to (TODO: something about this being non-religious?).  With that said, we should agree on a few things that, for the sake of the length of this article, will have to be accepted as givens. 

###TODO: Givens
1. The primary goal of software engineering is to create value.
  * I would argue that creating value is the primary goal of every endeavor, but that's a separate post.

###Defining Tech Debt
First things first, we should agree on what it is we're talking about.  You can say 'tech debt' in nine characters, just two syllables, and yet you're talking about a lot of stuff when you use that term.  Tech debt is that old system that is big, buggy, and still in use for various reasons; it's that area of the code base that has been poked and prodded for so long by so many people that it is a rats nest in to which no one wants to voyage; it's that quick hack you put in just the other day that made you cringe when you did it but doing it "the right way" would have taken weeks; it's that system that is otherwise fine but lacks any unit tests so making changes is a tight-rope walk; it's the system that was meant to be a prototype which is now used in production.  Tech debt is a lot of things.  To generalize this to a single definition is complicated.  The definition I have come up with is "tech debt is code which a reasonable engineer, in the present, wishes was different".  I'll agree that this definition is a little shaky as it is based on the subjective opinion of an imagined engineer, but it's what I'm going with.

###Ideas
* interest on tech debt (toxicity * churn)
* not just toxicity - overall design can be debt as well

TODO: above this line has been rewritten

###Tech Debt as a Tool
This is where this journey began for me.  I have been dealing with the concept of tech debt for a while, but only recently realized how perfectly the term debt applies to the concept.  For those who are not familiar, tech debt is a term used in software engineering to describe code which is (in some way) not ideal.  Perhaps the code is a knot of logic (spaghetti code), doesn't have any unit tests, or was written long ago using a methodology which has fallen out of favor.  Whatever the reason, it is code which the engineers that are maintaining it wish was different in some way.

It is easy to look on tech debt with an eye of scorn.  A lot of tech debt is found in areas of code which are old and were written by others.  Some of the disdain is certainly well deserved.  If thedailywtf.com has taught us anything it is that some programmers are capable of writing some creatively heinous code.  But not all tech debt should be seen as an abhoration.

First, as people visiting the past from the present (looking at code written previously) we have no idea what was going on at the time the code was written.  Even if we were the ones that wrote it, we don't stand a chance of remembering all of the context that ultimately led to the keystrokes to produce that code.  Perhaps the office environment was really stressful at the time, maybe there was a problem with the heat or A/C that made concentrating really difficult, or perhaps the author was too stressed thinking about the mortgage debt he was preparing to take on to contemplate the tech debt he was creating.  :-)

Secondly, there may have been a very good reason to take on the tech debt.  This segways in to the first realization on the path to generalizing the concept of debt.
For all you know if the author of the tech debt in question hadn't taken on the debt that he had, the company wouldn't have even been around to hire you.  Maybe you owe the author of that tech debt an apology.

* save time in active development (time to market)
* save time early on (uncertain future)
* save money early on (developers)


###Ideas
* Debt involved in writing this story (time, energy, calories, etc.)
* Reading directions (time debt)
* * Learning in general, although learning has immediate value of enjoyment
* Life gives you time, which you are free to spend, but you don't know how much you have
* * Spend it on whatever you want, take on debt to make best use of time
