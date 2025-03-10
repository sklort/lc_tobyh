# Strudel+Hydra Midterm
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

[My patch](# Second Strudel Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
//@title visualsnow
//@by tobyh

/////////
//HYDRA//
/////////

await initHydra()


noise(() => (Math.sin(time/4)+16)*100, .3)
.thresh([.01, .2, .3, .4, .5]
  .smooth(), .001)
.color([.1 ,.3, .5, .6, .7, 9]
  .smooth(), 0, [.9, .7, .6, .5, .3, .1]
  .ease('linear'))
.scrollY([.01 ,.1, 1, 5, 10]
  .smooth(), .02)
.scrollX([10, 5, 1, .1, .01]
  .ease('easeInSine'), .2)
.modulateKaleid(noise(
  () => (Math.sin(time)+.01)*.007),
  [.1, .2, .5, .75, 1, 4, 8]
  .ease('linear'))
.kaleid([.03, .05, .75, 1, 2, 4, 8]
  .smooth())
.modulateRepeatY(osc(() => Math.sin(time/2)), .1,
  [.1, .3, .5].smooth())
.pixelate([100, 300, 500].smooth(),
  [500, 300, 100].smooth())
.add(noise(() => (Math.sin(time/4)+20)*100), .5)
  .color([.9, .62, .5].smooth(), 0,
   [.2 ,.5, .6, .8].smooth())
.modulateKaleid(noise(
  () => (Math.sin(time/2)+.02)*.08),
  [.01, .02, .05, .1, .25, .5, .75]
  .ease('linear'))
.modulateScale(noise([.01, .1, .3, .5, 1]
  .smooth()), [.25, .5, 1].smooth())
.kaleid([8, 4, 2, 1, .5, .25]
  .smooth())
.pixelate([250, 350, 500].smooth(),
  [500, 400, 200].smooth())
.brightness([.1 ,.075, 0.05]
  .smooth(1))
.out()

////////////
//STRUDEL//
///////////

const density = slider(1, 0, 1, .01)
const kickSeed = slider(16.78, 0, 24, .01)
const bassIntensity = slider(1.13, 0.5, 3, 0.01)
const noiseLPF = slider(1493, 500, 4000, 1)
const sineDens = slider(0, 0, .75, .01)
const fmDens = slider(0, 0, .75, .01)
const percSeed = slider(4, 0, 24, 1)
const percDegrade = slider(0.64, 0, 1, .01)
const fmTimb = slider(0.76, 0, 4, .01)

//MIXER
const tone1 = slider(0.39, 0, 1, .01)
const tone2 = slider(0, 0, 1, .01)
const tone3 = slider(0, 0, 1, .01)
const tone4 = slider(0.27, 0, 1, .01)

const perc1 = slider(0, 0, 1, .01)
const perc2 = slider(0, 0, .5, .01)
const snare = slider(0.28, 0, 1, .01)

const chords = slider(0, 0, .6, .01)
const bass = slider(0, 0, 1, .01)
const noise1 = slider(0.3, 0, 1, .01)

stack(
  //tones
  freq ("800".mul("[1.5 | 2 | 3 | 4 | 6]"))
        .degradeBy(sineDens).adsr(".001: .1: 0: 0")
       .slow(2).gain(tone1),
  freq ("[812 | 1793 | 2091 | 2893]").segment(16).degradeBy(fmDens).slow("[8 | 16 | 32]")
    .sound("sine").adsr(".001: .1: 0: 0").gain(tone2).fm(fmTimb),
  freq ("[500 | 1025 | 912 | 1392]").segment(16).degradeBy(fmDens)
    .sound("sine").slow("[8 | 6 | 14]").adsr(".001: .2: 0: 0")
    .fm(fmTimb).fmh("[0 | .25 | .5 | 1 | 2]").gain(tone3),
  n("[6 | 9 | 11 | 14 | 17 | 21]").scale("C:chromatic").sound("sine")
    .degradeBy(sineDens).segment("[4 | 8 | 12]").slow("[6 | 8 | 12]")
    .adsr(".002: .3: 0: 0").gain(tone4),
  // // perc
  freq ("<1928 2500 3200 2152>").fast(32).degradeBy(percDegrade).ribbon(percSeed,1)
    .sound("sine").adsr(".001: .01: 0: 0")
    .penv([0, 6, 12, 18, 24]).lpf(1000).gain(perc1).fm(1),
  freq ("[500 | 830| 1028 | 1800 | 2100 | 2900]").sound("sine")
    .fast(32).penv(6).degradeBy(percDegrade).ribbon(percSeed, 1).pdecay(".01")
    .adsr(".01: .1: 0: 0").gain(perc2).fm("[0 | .25 | .5 | 1 | 2 | 3]")
    .fmh("[.5 | .7 | 1 | 1.5 | 2]"),
  //chords
  freq ("[250, 750, 1500] | [406, 709, 1356] | [448, 896.5, 672.4] | [120, 240, 320, 600]")
    .sound("sine").slow(2).degradeBy(.5).adsr("3: 8: 0: 0").crush("[6 | 8 | 10 | 12]")
    .delay(.5).delaytime("[.001 | .005 | .01 | .05]").delayfeedback(.9).phaser(8).lpf(750)
    .vib("[4 | 8 | 16 | 32]:[.01 | .03 | .75]").room(.5).roomsize(7).gain(chords),
  //snare
  sound("white").fast(16).degradeBy(.7).gain(snare)
    .adsr(".01: [.01 | .075 | .15]: 0: 0"),
  //kick
  freq ("[60]").sound("sine")
  .fast(32).degradeBy(density).ribbon(kickSeed, 1)
  .penv("[16 | 24 | 32]").pattack("0.01").pdecay(".001")
  .adsr(".01: .1: 0: 0").gain("[.5 | 1 | 1.6]").distort(1),
  //bass
  freq ("[40 | 50 | 60 | 70]").segment(4).sound("sine")
    .gain(bass).distort(bassIntensity).slow(2)
    .degradeBy(.5).adsr(".01: .1 : .7: .3")
  .penv("[6 | 12 | 18 | 24]").pdecay(.05),
  //noise
  sound("white").slow(2).degradeBy(.6).phaser("[1 | 4 | 2 | 8 | 16 | 32]")
    .gain(noise1).crush("[16 | 12 | 8]").fm("[0 | .5 | 1]")
    .fmh("[.5 | 1 | 2 | 4]").lpf(noiseLPF)
).room(.3).roomsize(8).postgain(.8).fast(.8)

```

[My patch](https://strudel.cc/?m9VwaHvuNDkP)

I've been listening to a lot of Ryoji Ikeda lately, and thus wanted to make a Ikeda inspired patch.
I also have visual snow, which makes me see static everywhere, so I wanted to use modulated TV static for my visuals.
I started out with the visuals, and mainly focused on creating modulation which didn't happen too frequently.
I used lots of .smooth() and Math.sin functions to make transitions smoother.
I also used a lot of geometric modulation, such as pixelate and kaleid.

For the patch, I started out with sine tones which I modulated with FM.
I added a white noise foundation which I modulated with phasers,
chords with modulation, a randomized kick, and a bass.
I added sliders to control randomization and mixing. 
