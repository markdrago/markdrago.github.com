---
layout: post
title: "A Pragmatic Exploration of Tech Debt"
title: "Refactoring the Very Idea of Tech Debt"
date: 2012-03-03 12:14
comments: true
published: false
categories: 
---

This post explores the concept of tech debt.  In particular I would like to disect the jumbled notion of tech debt and discuss each discreet concept in detail.  In some ways you can think of this essay as a refactoring of the idea of tech debt.

###Defining Tech Debt
{%pullquote%}
First things first, we should agree on what it is we're talking about.  The term tech debt gets used in a ton of different ways and situations.  Tech debt is that old system that is big, buggy, and still in use for various reasons; it's that area of the code base that has been poked and prodded for so long by so many people that it is a rats nest in to which no one wants to voyage; it's that quick hack you put in just the other day that made you cringe when you did it but doing it "the right way" would have taken weeks; it's that system that is otherwise fine but lacks any unit tests so making changes is a tight-rope walk; it's the system that was meant to be a prototype which is now used in production.  Tech debt is a lot of things.  To generalize this to a single definition is complicated.  The definition I have come up with is "{"tech debt is code which a reasonable engineer, in the present, wishes was different"}".  I'll agree that this definition is a little shaky as it is based on the subjective opinion of an imagined engineer, but it's what I'm going with.
{%endpullquote%}

###How Tech Debt is Born
There are many ways that tech debt comes in to being.  Lets start with the most obvious.

####I just stepped in a fresh pile of tech debt####
The kind of tech debt we tend to picture when we hear the word is that pile of code that, from the start, was written quickly and haphazardly.  Maybe the code was written by inexperienced engineers who were learning how to structure a large project as they went.  This kind of tech debt fits the name 'debt' very well.  It represents immediate cost savings (coding quickly, hiring less experienced engineers), with the pain of dealing with that cost savings later on.  It is also acquired accidentally.  That is, there is no conscious decision or open discussion about incurring this tech debt.  It is something that is discovered down the road.  Someone finally says, "Wow.  This code is a wreck.  Maybe we should've taken our time.", or "Who wrote this?" and the answer is "That intern that was the first guy to ever work on the project".

####If I knew then what I know now####
{%pullquote%}
Learning is good and we're all doing it.  Software engineering is still a young field.  We're all helping to define it.  This is one of the things that makes the field so exciting.  A few years from now I will have personally learned a lot about software engineering and the entire field will have changed in some interesting way.  Personal learning is to be embraced, not avoided, and the field is going to be changing whether you change with it or not.

{"Along with all of the benefits of learning comes tech debt."}  You know, that code you wrote before you learned that thing - or the code that we all wrote before the field valued that thing.  A good example of this is TDD (Test Driven Development).  I wrote a bunch of code before I learned about TDD (or unit testing in general).  Now I look at that code, which I was happy with at the time, and I see tech debt.  Another good example is language choice.  There was a time when new projects were written in perl, cold fusion, VB, ASP, etc.  At the time those projects began those languages were probably a reasonable choice.  Now those projects, at least through most engineers' eyes, would be seen as tech debt.  The field has moved on and there are just better options available to us now.
{%endpullquote%}
This kind of tech debt is very hard to predict for obvious reasons.  It's impossible to know what I'm only going to learn a few years from now.  It's also impossible to know what new idea will be valued by the field of engineering in a few years.  For those simple reasons you can't really avoid this kind of tech debt.  The best way to prolong the life of your work is to always be learning, experimenting, and researching the latest developments in the field.  I mean, I guess you could also just put your head in the sand and stop learning things, then you'll never run the risk of seeing your old work from a new perspective.  This kind of tech debt should carry no shame.  It's simply a cost of working and learning.

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

###Desirable Tech Debt
Finally, we arrive at the kind of tech debt that is the most controversial.  This is the tech debt that you take on consciously.  This is where you know there are a few ways to go about coding the solution you're working on and you consciously choose the quicker or easier way, knowing full well what you're doing.  This kind of tech debt is a shortcut that you take now and will have to deal with later.  This is true of pretty much all debt.  Lets compare this kind of debt to a mortgage.

When you take out a mortgage you are taking a shortcut.  Rather than slowly building up the stockpile of cash that you will need to buy a house in cash you're able to buy the house immediately.  This is nice because you'll be able to enjoy the house during the 20 years or so it would have taken you to save up the cash to buy the house without the mortgage.  The situation with tech debt is very similar.  You're taking a shortcut and enjoying the new feature more quickly than you would otherwise be able to enjoy it.  Depending on your business and the feature you're building this could have a profound impact on your business.

Just like taking out a mortgage, taking on tech debt can be a big decision.  It's important that you weigh the benefits that you'll be enjoying against the pain that you will be experiencing.  It's not okay to go traipsing through your code base creating havoc for little-to-no gain.  Likewise, it's not okay to always be demanding perfection and holding back otherwise realizable value.  There's a balance that needs to be struck.

####Repayment
{%pullquote%}
All debt has to be repaid and tech debt is no different.  It is absolutely critical that you have time set aside to pay down tech debt.  Trying to skimp on repayment of tech debt leads down one of two disasterous paths.  One path leads to a code base that is riddled with tech debt.  So many shortcuts have been taken and ignored that you can't even get the simplest of things done.  The other path leads to a beautiful code base, but doing everything perfectly has been an incredible burden.  While you were busy saving up to buy your first house your competition took out a mortgage, bought a house, has the whole thing beautifully furnished, is throwing a party, and has nearly paid back the loan already.  {"Having a plan set up to pay back tech debt lets you take important shortcuts."}
{%endpullquote%}

####Amortization Plan
{%pullquote%}
Along with debt comes interest payments.  {"The interest that you pay on tech debt is the loss in productivity that results from the tech debt's existence."}  The worse the tech debt, the higher the interest.  But how should we be comparing one chunk of tech debt with another?  The interest on tech debt should always be in terms of pain.  Code that everyone agrees is poorly designed, but that isn't generating bugs or being actively worked on, is not causing a lot of pain.  Inversely, code which at first glance seems reasonable, but is creating headaches for everyone that is working on it, is creating a lot of pain.  So, which tech debt should be paid back first?  Easy - the debt that has the highest interest payments / is causing the most pain.
{%endpullquote%}

###Final Payment
Debt can be a useful tool in financial planning and it can be a useful tool in software engineering.  Ultimately the job of software engineers (and really any employee) is to generate business value.  If you find yourself in the position where you can take on a reasonable amount of low-interest tech debt and deliver important value to the business you should be proud to make the decision to take it on.  Tech debt can be a powerful tool, and like all powerful tools, should be used wisely.  But it would be a shame to leave it unused.

