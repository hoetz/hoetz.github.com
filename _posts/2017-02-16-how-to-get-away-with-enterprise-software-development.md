---
layout: post
category : programming
tagline:
date: 2017-02-16 15:30:00 UTC 
tags : [programming]
title: How to get away with enterprise software development
---
{% include JB/setup %}

How to get away with enterprise software development
====================================================

0 - YAGNI
---------

Before we even write the first line of code, remember that not doing something
at all is occasionally a valid option. The
[YAGNI](https://en.wikipedia.org/wiki/You_aren't_gonna_need_it) principle may be
applied to various aspects of software development projects. Can we use an
existing library for Task X? Was feature Y really part of the specification
provided by the stakeholders? Did we use market research to figure out if
product Z we are about to create provides any meaningful value for the target
audience? You may be surprised how often developers rush in to "save the day"
just to find out that X is on nuget, Y was never really needed and Z is already
being rolled out by a competitor.

1 - Collaborate!
----------------

Communication is key and nothing beats face-to-face when it comes to
implementing a software solution. But as soon as at least one member of your
team is not sitting in the same room, things change. To be clear: if one member
of your team is collaborating online, everyone has to. Apps like Slack or
Microsoft Teams offer a great way to tie your workflow together but it is
important that the entire team commits to a set of tools before the project
begins.

2 - Scale your team
-------------------

[David Fowler](https://twitter.com/davidfowl/status/830574942320152578) recently
tweeted \>As a senior engineer, you have to decide if it's better to do things
yourself or help junior developers grow

which brings me to the often shunned topic of knowledge management. Transferring
personal knowledge to a colleague might be one of the hardest parts in your
career but the reward is a team that truly scales. By the time you realize that
you or a member of your team is a knowledge bottleneck you might already be
knee-deep in a customer project, so plan accordingly.

3 - Code Outside-in, code SOLID
-------------------------------

Ultimately, when starting to code, we should aim to produce clean and
maintainable code. The outside-in approach focuses on satisfying the needs of
stakeholders but I also like to apply it coding. It turns out that Visual Studio
has [pretty good
support](https://msdn.microsoft.com/en-us/library/dn872466.aspx) for sketching
out the flow of your program without implementing the actual methods right away
- a great way to do [TDD](https://www.pluralsight.com/courses/outside-in-tdd),
by the way. When you get down to the implementation it is prudent to adhere to
design principles like
[SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)) or
[DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) and yet, realizing
them is easier said than done. It's easy to tell that methods with more than 100
lines of code probably have a complexity problem and that the same method
shouldn't appear five times across your code base. But, for example, getting
inheritance or interfaces "right" is usually a tad more difficult.

I have found these basic tips pretty helpful: - keep your units of code small
and focused - work your way from outside (i.e. user interface) down to the
bottom layer - separate storage access code from your business logic and your
business logic from the user interface - (integration- / unit-) test the hell
out of everything you write

In the end, only writing code will help you improve writing even more code.

And [reading a good
book](https://www.amazon.de/Microsoft%C2%AE-NET-Architecting-Applications-PRO-Developer/dp/073562609X).

And getting [involved](https://www.github.com) with open source code.

4 - Git yourself a proper version control system
------------------------------------------------

If you are still using centralized source control systems like SVN or TFVC, you
might want to take a good look at [git](https://git-scm.com/). Besides being
used by major tech companies like Google, Microsoft or Netflix, it is easily the
best way to implement a smooth [feature branch
workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflows)
for your team, which is, in my opinion, a prerequisite for agile software
development.

5 - Build, Test, Deploy - Automate all the things
-------------------------------------------------

If you're reading this you've probably already written a console or web
application, built it in your favorite IDE, tested it on your local machine and
copied the binaries over to a file share or a web server. Enter
[DevOps](https://en.wikipedia.org/wiki/DevOps), a set of practices that
basically tells us to automate all the things we might have been doing by hand
for too long. With the advent of cloud based applications and development tools
it's become extremely simple to spin up a complete DevOps environment in no
time. But for smaller projects, even a [simple
script](https://github.com/hoetz/SimpleAD/blob/master/BuildRelease.ps1) that
builds a release version of your library and creates a nuget package is a first
step towards automation. Eventually, this kind of automation reduces friction
and increases confidence for you and your team.
