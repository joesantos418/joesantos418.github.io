---
layout: post
title:  "Should you deploy on Fridays? The definitive guide"
date:   2021-10-01 18:00:00 -0300
categories: software, deployment
---

#### The answer may be more complicated than you'd think

*Disclaimer: This post was originaly published on [Arquivei's engineering team's Medium](https://medium.com/engenharia-arquivei/should-you-deploy-on-fridays-the-definite-guide-b24cb16ad91c)*

First I came across a joke. Then it seemed like everywhere I looked there was
something about the issue of deploying on Fridays: memes, funny videos, serious
posts, rather aggressive arguments, and even websites that make a statement in a
very loud way about whether or not you should do it. A [quick search](https://www.google.com/search?channel=fs&client=ubuntu&q=should+you+deploy+on+friday)
will show you that everyone has an opinion on it and nobody wants to budge.
With such polarization, thousands of people (*coughs*, nobody) came to me for a
definitive answer. And it is "It depends".

Let's take the obvious out of the way first: You're more likely to have
something after work on Friday than on Monday or Wednesday. Sometimes even
something that cannot be postponed like a flight. Also if you have work that
must be done tomorrow, it's better if you're in the office tomorrow anyway.
Finally, big releases usually happen on Monday for strategic reasons so you're
unlikely to find something that has a critical time to market on Friday.

We should also note that when we ask this question, we are not talking about bug
fixes. Those will almost always be pushed whenever they are deemed ready.

People who say you shouldn't do it will argue that even if your process is
solid, bugs can slip through and make their way into production. Of course, they
are being kind and assuming every company follows good quality assurance
principles, and nothing is ever rushed, and everyone is always reviewing code
with a sharp eye, and thinking about every possible flow.
**EVEN THEN** bugs still can happen and they prefer to risk it from Mondays to
Thursdays.

People who say you should do it often argue that the previous group has a failed
process: the deliveries happen so rarely that they become a pain, their scope is
too big, or they simply aren't doing their job well enough (kids, play nice!).
The "yes" movement will respond with additions to the process like continuous
delivery and tips for planning your scope better.

Both sides have pretty compelling arguments, but they fail to handle nuance. You
can have CD, unit tests, integration tests, full coverage, code reviews, and
whatever else **AND STILL** fail. On the other hand, not all bugs in production
will cost you a head of hair or the weekend, nor every feature carries the same
risk.

At Arquivei we have test accounts in production for most projects. Right after
deployment, we go online and check if everything worked as expected, that's the
first sign that things will be okay. Then we give users some time to use the
updated flows. As a rule of thumb, we like to wait a few hours for users to go
through the new code and if nothing gets reported and our monitoring tools
remain calm, we feel like we'll be okay for good.

It's important to notice that we don't rely on users to report bugs and neither
should you. A good quality assurance process is essentials as is observability:
logs, alerts, dashboards, whatever it takes for you to know how healthy your
application is in time as real as possible. However, that could also fail and
when it does, the user will be the voice of that failure. We can only make that
probability very low, but it will always be above zero and we better be ready.

Of course that users won't have enough time to try what's new if we deploy at
4:30 pm on Friday and we prefer to start our weekend leaving behind code that
was validated by running smoothly in production. However, sometimes we can
validate that code very quickly (some flows have lots of users on it at all
times, for example) and in those situations, it's more likely that we will
deploy on a Friday.

Another thing to consider is the impact of the changes. The cost of an error is
not the same anywhere in the code: a typo on a landing page is not the same as a
division by zero in your commission calculation. Changes that contain more
expensive error potential are more likely to be postponed.

Also, some changes will show that they are broken way faster than others.
Integrations aren't always possible to validate in staging and your code that
"didn't change anything to do with that integration" can cause an error. Your
alerts and logs should flood your screen with the issue before it affects a lot
of people and you will know very quickly about it. Other errors may only be
caught a while later. The faster it is to detect a bug in the changes, the more
likely they are to be deployed on Friday.

Lastly, rolling back to a stable state is quick and easy for us. When errors
happen, it's usually one of the first things we do, but sometimes that requires
several rollbacks of different systems. Also, some changes have effects that are
easy to reverse, others will require queries in the production database or any
deeper investigation about which users were affected, for example. If the
changes that potentially hard to roll back, they get a second thought for end
of the week deliveries.

This is pretty much what I consider before deploying on a Friday or the late
hours of any afternoon, actually. I know that estimating the attributes that
guide this decision is not always easy or accurate. When in doubt I leave it for
the next Monday. We trust our process and we're not afraid of failing, but our
deliveries affect all stakeholders and they must be considered when deploying.
Every bug developers introduce results in stress for our support team, impacts
our sales team, and not only the developers, but the SREs have to work outside
of their planned sprint to fix it.

Thinking like this has allowed us to leave work without any worries for most
weekends (*other* reasons may still apply) no later than usual while keeping our
clients happy and the rest of our teammates in their regular schedule. All that
while delivering timely solutions.

I hope you take the time to evaluate what makes sense to your organization. Not
everything is black and white and making decisions considering the context will
often make your life easier in the future.

Thanks for reading.

Special thanks to [@brunocalza](https://twitter.com/brunocalza) and
[@lemuelroberto](https://twitter.com/lemuelroberto) for the review.