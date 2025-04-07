# First TidalCycles Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
d1 $ fast 1 $ s "<[gabba*2 gabba gabba gabba*2] [gabba gabba gabba gabba]>"
-- "[gabba ~ gabba ~]" "[gabba ~ ~ ~ ]" "<[gabba*2 gabba gabba gabba*2] [gabba gabba gabba gabba]>" "[gabba gabba gabba gabba*2 | gabba gabba gabba gabba]"
  # crush "[16 | 12 | 8 | 4 | 2]"
  # triode "[0 | 0.5 | 0.8]"
  # distort "[0.3 | 0.5 | 1]"
  # shape "[0.3 | 0.5 | 0.8]"
  # size "0.3"
  # coarse "[1 | 2 | 3 | 4 | 6 | 8]"
  -- # silence


xfade 1 $ s "[reverbkick reverbkick reverbkick reverbkick*2 | reverbkick reverbkick reverbkick reverbkick]"
  # shape "[0 | 0.5 | 0.7 | 0.8]"
  # triode "[0 | 0.5 | 0.8]"
  # distort "[0.25 | 0.5 | 0.75 | 1]"
  # crush "[16 | 12 | 6]"
  # squiz "[0 | 0 | 2 | 4]"
    -- # silence

d2 $ fast 1 $ s "~ [808oh | 808oh*2] ~ 808oh ~ [808oh | 808oh*2 | 808oh*4] ~ 808oh"
  # shape "[ 0.5 | 0.7 | 0.9]"
  # distort "[0.5 | 0.8 | 1]"
  # crush "[16 | 12 | 8 | 4]"
    -- # silence

d3 $ fast 1 $ s "[~ ~ cp*2 ~ ~ cp cp cp]"
  # squiz "[2 | 4 | 8]"
  # shape "[0.2 | 0.5 | 0.7]"
  # distort "[0.3 | 0.6]"
  # crush "[16 | 12 | 8 | 4]"
    -- # silence

-- "~ ~ [cp | ~] [~ | cp] ~ ~ [~ | cp] ~"
-- "[~ cp cp cp ~ cp cp cp*2] "[~ ~ cp*2 ~ ~ cp cp cp]"

d4 $ slow 4 $ note "[c | ~ | ab | f] ~ [~ | bb | eb | gb | ~] ~"
  # sound "supernoise"
  # octave "[ 3 | 4 | 5]"
  # squiz "[4 | 8 | 12 | 16]"
  # distort "[0 | 0.3 | 0.5 | 0.8]"
  # shape "[0 | 0.3 | 0.5 | 0.8]"
    -- # silence

d5 $ degradeBy 0.3 $ fast 4 $ note (arp "[converge | diverge | thumbup | pinkyup]" "<f'sevenSharp5flat9>")
  -- # speed (rand*12)
  # octave "[3 | 4 | 5]"
  # sound "superhoover"
  # crush "[3 | 2 | 1]"
  # distort "[0 | 0.3 | 0.5 | 0.75 | 1]"
  # coarse "[4 | 6 | 8 | 16]"
  # lpf 10000
  # freeze "[0 | 0.5 | 1 | 2]"
    -- # silence

  hush


setcps (184/60/4)


```
For this patch, I wanted to make a hardcore beat with very basic, noisy elements. The groove can be a bit odd with all the randomization, but it works kinda!
I used a hardcore kick, crossfaded with a reverbkick, then openhats, claps, a noise synth, and a superhoover.
Most of the debugging I did was just familiarizing myself with different effect/transformation parameters, such as the distort compared to shape.
The most trouble I had was using arp, as I had thought it could use scales but figured out it only uses chord shapes.
With all the elements it becomes really muddy and really grating to listen to, but sometimes it sounds cool lol
