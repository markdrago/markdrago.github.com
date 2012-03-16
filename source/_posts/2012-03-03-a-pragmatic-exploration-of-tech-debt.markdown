---
layout: post
title: "A Pragmatic Exploration of Tech Debt"
date: 2012-03-03 12:14
comments: true
published: false
categories: 
---

This post explores the concept of tech debt.  In particular I would like to disect the jumbled notion of tech debt and discuss each discreet concept in detail.  In some ways you can think of this essay as a refactoring of the idea of tech debt.

###Defining Tech Debt
{%pullquote%}
First things first, we should agree on what it is we're talking about.  You can say 'tech debt' in nine characters, just two syllables, and yet you're talking about a lot of stuff when you use that term.  Tech debt is that old system that is big, buggy, and still in use for various reasons; it's that area of the code base that has been poked and prodded for so long by so many people that it is a rats nest in to which no one wants to voyage; it's that quick hack you put in just the other day that made you cringe when you did it but doing it "the right way" would have taken weeks; it's that system that is otherwise fine but lacks any unit tests so making changes is a tight-rope walk; it's the system that was meant to be a prototype which is now used in production.  Tech debt is a lot of things.  To generalize this to a single definition is complicated.  The definition I have come up with is "{"tech debt is code which a reasonable engineer, in the present, wishes was different"}".  I'll agree that this definition is a little shaky as it is based on the subjective opinion of an imagined engineer, but it's what I'm going with.
{%endpullquote%}

###How Tech Debt is Born
There are many ways that tech debt comes in to being.  Lets start with the most obvious.

####I just stepped in a fresh pile of tech debt####
The kind of tech debt we tend to picture when we hear the word is that pile of code that, from the start, was written quickly and haphazardly.  Maybe the code was written by inexperienced engineers who were learning how to structure a large project as they went.  This kind of tech debt fits the name 'debt' very well.  It represents immediate cost savings (coding quickly, hiring less experienced engineers), with the pain of dealing with that cost savings later on.  It is also acquired accidentally.  That is, there is no conscious decision or open discussion about incurring this tech debt.  It is something that is discovered down the road.  Someone finally says, "Wow.  This code is a wreck.  Maybe we should've taken our time.", or "Who wrote this?" and the answer is "That intern that was the first guy to ever work on the project".

####If I knew then what I know now####
{%pullquote%}
Learning is good and we're all doing it.  Software engineering is still a young field.  We're all helping to define it.  In my opinion this is what makes the field so exciting.  A few years from now I will have personally learned a lot about software engineering and, it is my belief that, the entire field will have changed in some interesting way.  Personal learning is to be embraced, not avoided, and the field is going to be changing whether you change with it or not.

{"Along with all of the benefits of learning comes tech debt."}  You know, that code you wrote before you learned that thing - or the code that we all wrote before the field valued that thing.  A good example of this is TDD (Test Driven Development) or unit testing in general.  I wrote a bunch of code before I learned about TDD (or unit testing in general).  Now I look at that code, which I was happy with at the time, and I see tech debt.  Another good example is language choice.  There was a time when new projects were written in perl, cold fusion, VB, etc.  At the time those projects began those languages were probably a reasonable choice.  Now those projects, at least through most engineers' eyes, would be seen as tech debt.  The field has moved on and there are just better options available to us now.
{%endpullquote%}
This kind of tech debt is very hard to predict for obvious reasons.  It's impossible to know what I'm only going to learn a few years from now.  It's also impossible to know what new idea will be valued by the field of engineering in a few years.  For those simple reasons you can't really avoid this kind of tech debt.  I mean, I guess you could put your head in the sand and stop learning things, then you'll never run the risk of seeing your old work from a new perspective.  This kind of tech debt should carry no shame.  It's simply a cost of working and learning.

####Two's company, three's a crowd####
Decisions that were perfectly reasonable given the environment of a few years ago may seem like a folly in the present.  A good example of this is code sharing.  Say you have two projects, a web frontend and some backend job processing.  Also you have some utilities that each project could benefit from using.  It makes sense to put those utilities in a shared project which both projects depend on.  But then both projects are accessing the database, and touching the same tables, and caring about similar things, somethings happen automatically during a batch job and are also triggerable in the web frontend.  All of these things end up getting put in to the shared project.  There is a scale where this solution is perfectly appropriate.  Maybe there are just a few engineers and the size of the shared project is small enough that it's palatable.  Any other solution would introduce a lot of overhead and the pain caused by this shared project is manageable.

{%pullquote%}
But then your business is successful, you're hiring engineers left and right, and they're all writing code and putting it in to that shared project.  At some point you look around and you realize that the shared project is now the biggest project that you have and it's getting increasingly hard to deal with and manage.  {"You made a resonable decision back when there were two engineers, which slowly, as you grew, became tech debt."}
{%endpullquote%}

The key thing is to recognize this as a problem and address it at the right time.  Lets say that the proper solution for this is to switch to an SOA (Service Oriented Architecture) model where you minimize (eliminate?) shared business logic and separate areas-of-concern in to individual services.  Starting the project out from the get-go in this model would probably have been a mistake.  At that point you don't know where the business is going and you have no idea what kind of problems you'll be facing a few years down the road. Also, the best way of managing shared logic for a small team and a small project is almost certainly different than the best way of doing it for a large team and a large project.  Now, as the code base grows and the team grows, at some point you have to revisit this decision and start making the switch.  There is no mistake in choosing what is right for your team and project in the present, the mistake is made when the pain becomes real and you don't address it.

####Wait, we're what kind of company now?####
This kind of tech debt is similar to the previous, but rather than the team changing, it is when the business changes.  An example of this is Flickr.  Flickr started as an MMORPG called "Game Neverending" that had some ability to post and share photos [en.wikipedia.org/wiki/Flickr#History].  Even after pivoting and focussing on becoming a photo sharing site, a main component of Flickr was a live chat room.  All of this code was based on the original game code base.  Over time Flickr addressed that problem and migrated off of the old code base.  But for a period of their history their (perhaps) well-designed game code was powering a photo sharing site.  That's crazy and that's tech debt.

You could argue that you'll be able to handle changes that your company may make in the future by having well defined abstractions in your code.  But I don't think anyone can reasonably argue that they would have written the proper abstractions in a game such that when the company decided to focus on photo sharing the code would have remained beautiful and well architected.

{% pullquote %}
Adding abstractions is an important practice in designing any system.  But there is a cost associated with every abstraction that you add.  Prematurely adding layers of abstraction is especially dangerous as you're likely to spend more time adding the abstraction layer and, if you do not correctly predict the future, you're ultimately going to have to clean up both the main business logic and the abstraction layer.  In trying to avoid tech debt you may very well be creating even more.  In my opinion layers of indirection should be added once you have the second thing that will benefit from that abstraction.  That's not a hard and fast rule as there are plenty of times where common sense and just good engineering necessitates an abstraction.  {""Premature abstraction is the yin to premature optimization's yang."  --Kent Beck"}
[http://twitter.com/#!/KentBeck/statuses/167620773337505793]
{% endpullquote %}

####Hey, could you go in to my toolbox and pass me my tech debt####

TODO: using tech debt as a tool

TODO: process which focuses on tech debt
TODO: concept of interest (pain = level + frequency)

TODO: wrap it up

* Sloppiness (save money now, deal with debt later)
  * Rushing
  * Inexperienced Engineers
* Learning
  * Can't be avoided - we're all learning, expanding the field, hard to predict, shouldn't be ashamed
  * TDD
  * Language choice (perl, cold fusion, vb)
* Scope of business and engineering team grows
  * sharing code -> SOA
* Business needs changing
  * extremely hard to predict (example, flickr started as an MMORPG called 'Game Neverending', even after moving to focus on photos a live chat room was a main feature of the site - ultimately scrapped [en.wikipedia.org/wiki/Flickr#History])
  * overengineering to try and predict future
    * especially dangerous b/c you're paying now and likely to incur debt and thus pay later as well
    * kent beck: 'premature abstraction is the yin to premature optimization's yang' [http://twitter.com/#!/KentBeck/statuses/167620773337505793]
* Personnel changing - grow from 3 engineers to 10, acquisition, new engineers may have different background
  * some tech debt is subjective
    * language choice
    * tdd
* Tech debt as a tool
  * concious decision - deliver value early
  * amount of tech debt is acceptable - learning, mvp
  * only reasonable when a process is in place to clean up tech debt
    * leads in to next section about interest (pain - how bad vs. how frequent)

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
