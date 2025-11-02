---
layout: post
title: 'Math Is Fun'
date:   2025-11-02 19:13:23 -0400
categories: programming
---

# When do the minute and hour hands overlap?

Sitting in church gives my mind time to wander. On my better days, I think about divine matters and perhaps attempt to take stock of my spiritual state and progress. Just as often, I am restless, and my mind looks for more practical things to do. Sometimes I find a puzzle or problem that gives me something to chew on in the quiet. Long ago (likely staring at my watch) I stumbled upon this question - when would the hour and minute hands on a watch overlap? In other words, what time(s) would a clock show when this happened?

For years I would forget all about this question, only thinking to ponder it occasionally on Sunday mornings. I did this many times, pondering in the moment but never working it out all the way. Finally, my annoyance rose high enough that I remembered later that day. I sat down at home determined to solve the problem. This was a few weeks ago. I put pen to paper determined to crack it. This is a rough description of how I solved it:

## Attempt 1:
My gut reaction answer was - well - on the hour! As in 1 o'clock, 2 o'clock, etc. The error here is almost instantly apparent. At 1 o'clock the minute hand is at 12, but the hour hand is at 1. Oops. Nevermind. So obviously, this doesn't work. I've posed this question to others and heard a similar response, which helped soothe my ego some.
Ok, so when? Let's pick a value and work backwards to the general solution. How about 1:15? Nope. The minute hand is already way past the hour hand. What about 1:10? The minute hand is at 2 and the hour hand is at 1... and change. Closer, but hard to say for sure. We can maybe approximate the value but we're going to need math to find the actual answer.

Observation: The position of the hour hand is *dependent* on the position of the minute hand. The position of the minute hand is *independent* of the position of the hour hand. I'm not sure if this is profound or not.

Observation: Calculating the minute hand position in this way 'quanitizes' it. It treats it as having only discrete values. Obviously wrong, but worth noting that we'll need functions that describe continous values.

## Attempt 2:



Some conclusions:
- I continue to not fully grasp why the roots of an equation are of particular interest. In this case, the roots aren't paritcularly interesting. Here they equate to 'when are the hands pointing at zero.' Fair enough. But that's pretty easy. I want to know when they are touching.

I expected the answer to be a clean answer. Ideally whole, or at least rational. I guess it's technically rational, but with a repeating decimal. As a math cro-mag, it felt less 'done' than I had hoped.

After finding the answer, I realized a *much* simpler way to do it. I could simply take the number of total minutes in a rotation (60) and divide it by the number of overlaps in 12 hours (11). This gives the same answer, and intuitively it makes sense. I'm not sure it's feasible to intuit that there are 11 overlaps, however. That seems pretty hard. It's probably not realistic to imagine backing into that answer using that method on the first try.


