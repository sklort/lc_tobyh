# Second TidalCycles Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
-- birds
d1
  $ slow 1
  $ s "birds"
    # squiz "[2 | 4 | 8 | 16 | 32]"
    # fshift (rand * 5000)
    # freeze (5)
    # room 0.5
    # size 0.5
    # smear "[1 | 2 | 3 | 4 | 5]"
    # delay 0.5
    # delayt "[200 | 300 | 400]"
    # delayfb 0.3
    # gain "[0.5 | 1 | 1.5]"

-- tts base
d2
  $ degradeBy 0.5
  $ slow "[16 | 20 | 24]"
  $ s "alphabet" <| n (shuffle 8 $ run 26)
    # gain 0.5
    # squiz "[0 | 0 | 2 | 4]"
    # freeze 5
    # delay 1
    # delayt "[300 | 400 | 500 | 600]"
    # delayfb "[0.3 | 0.4 | 0.5 | 0.6]"
    # smear "[0 | 0.5 | 1 | 2]"
    # crush "[16 | 12 | 8 | 4]"
    # room 0.7
    # size 0.9

-- random stingers
d3
  $ fast 2
  $ degradeBy 0.9
  $ s "[circus:1 | circus:2 | circus:3]"
    # squiz "[2 | 4 | 8 | 16]"
    # freeze 3
    # smear "[1 | 2 | 3 | 4 | 5]"
    # delayt "[50 | 100 | 200]"
    # delay "[0 | 0.25 | 0.5]"
    # room 0.5
    # size 0.3
    # lpf 4000
    # gain 0.5

-- loud but smeared
d4
  $ degradeBy 0.8
  $ randslice 4
  $ s "[cosmicg:2 | cosmicg:3 | cosmicg4 | cosmicg:15]"
    # gain 0.5
    # smear "[1 | 2 | 3 | 4 | 5]"
    # squiz "[0 | 2 | 8 | 16]"


-- crows
d5
  $ degradeBy 0.75
  $ s "[crow:1 | crow:2]"
    # smear "[0 | 0.5 | 1 | 2 | 3 | 4]"
    # room 0.9
    # dry 0
    # size 0.75
    # gain 0.65

-- tts
d6
  $ degradeBy 0.5
  $ slow "[8 | 12 | 16 | 24]"
  $ s "diphone" <| n (run 38)
    # fshift "[0 | 1000 | 5000 | -1000 | -5000]"
    # lpf 10000
    # att "[0 | 5 | 10 | 20]"
    # freeze "[0 | 1]"
    # smear "[5 | 8 | 10]"
    # coarse "[4 | 8 | 12]"
    # dry 0
    # room 0.8
    # size 0.95

-- percs
d7
  $ slow "[1 | 2 | 4]"
  $ degradeBy 0.5
  $ s "e" <| n (run 8)
    # lpf 4000
    # coarse "[8 | 12 | 16]"
    # delayt "[1 | 2 | 3 | 20 | 50]"
    # delay "[0 | 0.1 | 0.2 | 0.3]"
    # delayfb "[0 | 0.25 | 0.5]"
    # gain "[0.3 | 0.5]"
    # dry 0
    # room 1
    # size 0.05

-- low koyis sample
d8
  $ fast "[1 | 2 | 4]"
  $ degradeBy 0.6
  $ loopAt "[4 | 8 | 12]"
  $ s "koy"
    # smear "[0.5 | 0.7 | 1 | 2]"
    # lpf 2000
    # dry 0.25
    # crush "[12 | 8 | 6]"
    # size 0.98
    # room 0.8

-- toy piano
d9
  $ degradeBy 0.5
  $ slow "[8 | 12 | 16]" $ s "toys" <| n (run 13)
    # fshift (rand * 1000)
    # smear "[0.5 | 1 | 2]"
    # squiz "[0 | 2 | 4]"
    # lpf 6000
    # room 0.5
    # dry 0
    # size 0.5
    # gain 0.5

-- merry christmas :)
d10
  $ degradeBy 0.75
  $ loopAt "[2 | 4 | 8 | 16 | 32]"
  $ slow 1
  $ s "xmas"
    # fshift (rand * 500)
    # room 0.25
    # size 0.9
    # lpf 2000
    # crush "[16 | 12 | 8 | 4]"
    # smear "[0 | 1 | 2]"
    # delay 0.5
    # delayt "[300 | 500 | 750]"
    # delayfb "[0.2 | 0.3 | 0.5]"



-- random tones
d11
  $ degradeBy 0.25
  $ slow 3
  $ freq "[136 | 283 | 403 | 639 | 1029 | 1830]"
    # s "superfork"
    # rel 1000
    # attack "[0 | 2.5 | 5]"
    # accelerate "[0 | 0.1 | 0.3 | 0.5]"
    # room 1
    # dry 0
    # size 0.85
    # crush "[12 | 10 | 8 | 6]"
    # lpf 4000
    # vowel "[a | e | i | o | u | p | k | q | ~ | ~ | ~]"

```
For this patch, I initially wanted to make an ambient piece that gradually changes in very subtle ways.
I started looking through the sample library and found a bird sample, which I thought would be a long loop.
However, it was very short, and so I started to screw around with audio effects, and eventually just made a weird sound.
I kept making these weird sounds until it started to sound creepy, experimenting with loopAt, distortions, time based effects, and frequency shifting.
The last piece I added was a physical model of a tuning fork which randomly plays notes.
I attempted to create a variable which would store randomized variables throughout a range since and then calling that variable inside the synth, since putting a rand inside the synth wasn't working.
However, I could not figure out how to make it work - I'll likely have to experiment with structs and I found some posts on the forum which sound like they'll help :)
