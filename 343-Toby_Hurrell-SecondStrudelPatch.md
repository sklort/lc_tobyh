# Second Strudel Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
stack(
  n (rand.range(0,24).segment(16)).scale("C:lydian").slow(2).degradeBy(.6).sound("triangle").adsr(".05: .02: 0: .5").lpf(1000).gain(.5),
  n (rand.range(0,12)).segment(16).scale("G:major").slow(2).lpf(800).degradeBy(.6).sound("sine").adsr(".2: .01: 0: .3").gain(.5),
  n (rand.range(0, 24).segment(16)).scale("D:mixolydian").slow(3).lpf(900).degradeBy(.85).sound("triangle").adsr(".5: .2: .5: .3").gain(.5),
  n (rand.range(-24,0)).segment(32).scale("C:chromatic").segment(32).slow(4).degradeBy(.75).lpf(600).sound("sine").adsr(".05:.1:.75:.3 ").gain(.7),
  n ("[[1, 3, 5] | [2, 4, 6] | [3, 5, 7] | [2, 5, 7] [ 1, 6, 3]]").scale("G:major").slow(4).sound("sine").degradeBy(.85).lpf(600).adsr("1:1:0:.5").gain(.5)
).room(.75).lpf(1000).postgain(.5).fast(sine)
```

[My patch](https://strudel.cc/?m9VwaHvuNDkP)

For this patch, I wanted to experiment with somewhat harmonious, randomized pitch collections.
I started out with some basic sine and triangle waves, in random ranges, and closely related scales.
I then added another sine, and a chromatic bass generator.
To balance these out, I assigned each one their own speeds and degradeBy's.
I then gave each an adsr, and after hearing how each one blended, I put in a chord generator.
It started reminding me of a csound generative patch I did a while ago, which had a lot of reverb and speed variation.
As such, the last thing I did was put in a reverb and modulated the speed with a .fast(sine) to give it some swells and spacing. 
