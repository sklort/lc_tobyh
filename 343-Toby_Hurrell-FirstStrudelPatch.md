# First Strudel Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
stack ("[bd ~ ~ ~ | bd bd ~ ~ | ~ bd ~ bd| bd ~ ~ ~] [bd? ~ ~ ~ | bd? ~ ~ bd!2?] [bd ~ ~ ~] [bd ~ ~ ~ | bd ~ bd bd]",
       "[<bd sd> ~ ~ ~] [bd ~ ~ ~] [bd ~ ~ ~] [bd? ~ ~ ~]",
       "[bd ~ ~ ~ | bd!2 ~ ~ bd] [bd? ~ ~ ~] [bd ~ ~ ~] [bd ~ ~ ~]",
       "[~ ~ ~ ~] [~ ~ sd ~] [~ ~ ~ sd] [ ~ ~ sd ~]",
       "[~ ~ ~ sd? | sd? sd? sd?] [~ ~ sd ~] [~ ~ ~ sd? | ~ ~ ~ sd | ~ ~ sd?] [ ~ ~ sd? ~ | ~ ~ sd sd!2? | ~ ~ sd? ~]",
       "[~ ~ oh ~] [~ ~ oh ~] [~ ~ oh ~] [~ ~ oh? oh | ~ ~ oh oh]",
       "[hh? hh? hh? hh? | hh? hh? hh? hh? | hh hh hh] [hh ~ ~ hh | ~ ~ ~ ~ | hh? hh? hh?] [hh? ~ ~ ~] [~ ~ ~ ~]",
      ).s().fast(1.25) 

```

[My patch](https://strudel.cc/?6XEPHrz1pbRA)

For my patch, I tried to make a sort of dembow beat with lots of randomization.
I mostly used the | random segment picker and the ? random silence. I also experimented with putting triplets/different meters in.
To emphasize certain beats, and to create interlocking rhythms, I layered the same instrument over itself multiple times.
I then used the random silence to create differences in the strength of the beat hits, for instance with the bd and sd segments.
One of the problems I ran into was that I tried to make a new stack with an AlmostNever function to randomly play in different meters.
However, I didn't know how to implement multiple stacks, so I just embedded the other meters inside the main stack.
