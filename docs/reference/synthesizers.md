---
title: Synthesizers
id: synthesizers
---

**SuperDirt** is installed along with an extensive list of *default* audio effects and synthesizers. Note that you can also extend this list by adding your own synthesizers and audio effects to the audio engine. For instance, check out the [Mutable Instruments](https://club.tidalcycles.org/t/mutable-instruments-ugens/2730) or the [SynthDefs for Tidal](https://club.tidalcycles.org/t/synthdefs-for-tidal/1092) threads on the **Tidal Club** forum.


## Parameters available for all synthesizers

| Parameter | What it adjusts            | Range   | Default value                |
| --------- | -------------------------- | ------- | ---------------------------- |
| `sustain` | Overall envelope timescale | 0 - ??  | 1                            |
| `pan`     | Position in space          | 0 - 1   | 0.5                          |
| `freq`    | Tuning                     | ?? (Hz) | 440 (unless specified below) |


## Additive synthesis
### Supergong

An example of additive synthesis, building up a gong-like noise from a sum of sine-wave harmonics. Notice how the envelope timescale and amplitude can be scaled as a function of the harmonic frequency. 

| Parameter    | What it adjusts                     | Range  | Default value |
| ------------ | ----------------------------------- | ------ | ------------- |
| `voice`      | Provides something like a tone knob | 0 - ?? | 0             |
| `decay`      | How the harmonics decay             | 0 - ?? | 1             |
| `accelerate` | Pitch glide amount                  | 0 - ?? | 0             |

```c
d1 $ n (slow 2 $ fmap (*7) $ run 8) 
  # s "supergong" 
  # decay "[1 0.2]/4" 
  # voice "[0.5 0]/8" 
```

## Substractive synthesis
### Supersquare, supersaw and superpwm

A Moog-inspired family of synths with common parameters:
- `supersquare`: square-wave synth; variable-width pulses with filter frequency modulated by an LFO.
- `supersaw`: sawtooth synth; slightly detuned saws with triangle harmonics, filter frequency modulated by LFO.
- `superpwm`: PWM synth; pulses multiplied by phase-shifted pulses, double filtering with an envelope on the second.

The only parameter which means different things per synth is `voice`:

| Synth         | What `voice` controls            | Range                                          | Default value |
| ------------- | -------------------------------- | ---------------------------------------------- | ------------- |
| `supersquare` | Pulse width                      | 0 - 1 (exactly zero or one will make no sound) | 0.5           |
| `supersaw`    | Relative phase and detune amount | 0 - 1                                          | 0.5           |
| `superpwm`    | Phase shift rate                 | 0 - 1                                          | 0.5           |

The common parameters are:

| Parameter    | What it adjusts                                                                        | Range  | Default value |
| ------------ | -------------------------------------------------------------------------------------- | ------ | ------------- |
| `decay`      | Length of decay                                                                        | 0 - ?? | 0             |
| `accelerate` | Pitch glide amount                                                                     | 0 - ?? | 0             |
| `semitone`   | How far off in pitch the secondary oscillator is (need not be integer)                 | 0 - ?? | 12            |
| `resonance`  | Filter resonance                                                                       | 0 - ?? | 12            |
| `lfo`        | How much the LFO affects the filter frequency                                          | 0 - ?? | 1             |
| `rate`       | LFO rate                                                                               | 0 - ?? | 1             |
| `pitch1`     | Filter frequency scaling multiplier, the frequency itself follows the pitch set by “n” | 0 - ?? | 1             |

### Superchip

Uses the Atari ST emulation *UGen* with 3 oscillators:

| Parameter    | What it adjusts                                                    | Range | Default value |
| ------------ | ------------------------------------------------------------------ | ----- | ------------- |
| `slide`      | Linear frequency glide                                             | ???   | 0             |
| `rate`       | How many times `slide` is repeated (can be fractional or negative) | ???   | 1             |
| `accelerate` | For an overall glide                                               | ???   | 0             |
| `pitch2`     | The ratio of harmonics                                             | ???   | 2             |
| `pitch3`     | The ratio of harmonics                                             | ???   | 3             |
| `voice`      | Variations in the levels of the 3 oscillators                      | ???   | 0             |

### Superhoover

Hoover, adapted from [Wouter Snoei](http://superdupercollider.blogspot.com/2009/06/more-dominator-deconstruction.html)’s implementation:

| Parameter    | What it adjusts                                                                   | Range | Default value |
| ------------ | --------------------------------------------------------------------------------- | ----- | ------------- |
| `slide`      | Amount of initial pitch glide (positive slides up in pitch, negative slides down) | ???   | 0             |
| `decay`      | Envelope shape                                                                    | ???   | 0             |
| `accelerate` | Constant pitch glide amount                                                       | ???   | 0             |

### Superzow

Phased saws:

| Parameter    | What it adjusts                     | Range | Default value |
| ------------ | ----------------------------------- | ----- | ------------- |
| `decay`      | Envelope shaping                    | ???   | 0             |
| `accelerate` | Pitch bend                          | ???   | 0             |
| `slide`      | How fast it moves through the phase | ???   | 1             |
| `detune`     | Oscillator detuning                 | ???   | 1             |

### Supertron

Feedback PWM:

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |
| `voice`      | Number of voices   | ???   | 0             |
| `detune`     | Detune amount      | ???   | 0             |

```c
d1 $ s "supertron" 
  # octave 3 
  # accelerate "0.2" 
```

### Superreese

Vaguely Reese-like synth:

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |
| `voice`      | Number of voices   | ???   | 0             |
| `detune`     | Detune amount      | ???   | 0             |

### Supernoise

Digital noise in several flavors with a bandpass filter.

### Superstatic

Impulse noise with a fadein/fadeout.

| Parameter    | What it adjusts                                                                                        | Range | Default value |
| ------------ | ------------------------------------------------------------------------------------------------------ | ----- | ------------- |
| `voice`      | Noise type: 0 - digital noise (`n` controls rate), 1 brown + white noise (`n` controls knee frequency) | ???   |               |
| `accelerate` | Causes glide in n, “rate” will cause it to repeat                                                      | ???   |               |
| `pitch1`     | Scales the bandpass frequency (which tracks “n”)                                                       | ???   |               |
| `slide`      | Works like accelerate on the bandpass                                                                  | ???   |               |
| `resonance`  | Filter resonance                                                                                       | ???   |               |

### Supercomparator

| Parameter    | What it adjusts                                                                        | Range | Default value |
| ------------ | -------------------------------------------------------------------------------------- | ----- | ------------- |
| `voice`      | Scales the comparator frequencies, higher values will sound “breathier”                | ???   | 0.5           |
| `decay`      | ???                                                                                    |       | 0             |
| `accelerate` | Pitch glide amount                                                                     | ???   | 0             |
| `resonance`  | Filter resonance                                                                       | ???   | 0.5           |
| `lfo`        | How much the LFO affects the filter frequency                                          | ???   | 1             |
| `rate`       | LFO rate                                                                               | ???   | 1             |
| `pitch1`     | Filter frequency scaling multiplier, the frequency itself follows the pitch set by “n” | ???   | 1             |

## Physical modelling
### Supermandolin

Physical modeling of a vibrating string, using a delay line (`CombL`) excited by an intial pulse (`Impulse`). To make it a bit richer, I’ve combined two slightly detuned delay lines:

| Parameter    | What it adjusts                | Range | Default value |
| ------------ | ------------------------------ | ----- | ------------- |
| `sustain`    | Changes the envelope timescale | ???   | 1             |
| `accelerate` | Pitch glide amount             | ???   | 0             |
| `detune`     | Detune amount                  | ???   | 0.2           |

### Superpiano

Hooking into a nice synth piano already in **SuperCollider**:

| Parameter  | What it adjusts                       | Range | Default value |
| ---------- | ------------------------------------- | ----- | ------------- |
| `velocity` | Affects how hard the keys are pressed | ???   |               |
| `sustain`  | Controls envelope and decay time      | ???   |               |
| `detune`   | Detune amount                         | ???   | 0.1           |
| `muffle`   | ???                                   |       | 1             |
| `stereo`   | Stereo amount                         | ???   | 0.2           |

### Superfork

Tuning fork from Ben Gold’s experimentation and from “On the acoustics of tuning forks”, Rossing Russell and Brown:

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |

### Superhammond

Hammond B3 sim. Frequency adjustments courtesy of [Tom Wiltshire](https://electricdruid.net/):

| Parameter | What it adjusts                                            | Range | Default value |
| --------- | ---------------------------------------------------------- | ----- | ------------- |
| `perc`    | Percussion strength (around 0.7 / 1.2 on vintage Hammonds) | ???   | ???           |
| `percf`   | Percussion frequency (2 / 3 on vintage Hammonds)           | ???   | ???           |
| `decay`   | Percussion decay (around 0 / 1 on vintage Hammonds)        | ???   | ???           |
| `vibrato` | Vibrato strength                                           | ???   | ???           |
| `vrate`   | Vibrato rate                                               | ???   | ???           |

`vibrato`, `vrate`, `perc`, `percf` are new parameters you’ll need to define in Tidal if you want to change them.

`voices` are drawbar presets:

* **0.** bass violin 16’
* **1.** tibia 8’
* **2.** bassoon 8’
* **3.** french trumpet 8’
* **4.** string ensemble
* **5.** Blues
* **6.** Jazz 1
* **7.** Full Shout
* **8.** Bro’ Jack
* **9.** Jazz 2

### Supervibe

Vibraphone simulation, adapted with some help from Kevin Larke’s thesis Real Time Vibraphone Pitch and Timbre Classification:

| Parameter    | What it adjusts                                                 | Range | Default value |
| ------------ | --------------------------------------------------------------- | ----- | ------------- |
| `decay`      | Use larger values to damp higher harmonics                      | ???   | 0             |
| `velocity`   | Higher velocity will brighten the sound a bit                   | ???   | 1             |
| `accelerate` | For a linear pitch bend                                         | ???   | 0             |
| `modamp`     | Amplitude of the tremolo (0-2 is OK)                            | ???   | 1             |
| `modfreq`    | Frequency of the tremolo                                        | ???   | 7             |
| `detune`     | Adjusts a high harmonic to give the sound a different character | ???   | 0             |

## FM synthesis - SuperFM

SuperFM is a 6-op FM synth (**DX7**-like). It works a bit different from the original **DX7**. Instead of algorithms, you can set the amount of modulation every operator receives from other operators and itself (feedback), providing a virtually endless number of possible combinations (algorithms). 

The synth's author [did an online workshop](https://www.youtube.com/watch?v=REgE33Esy2Q) explaining in depth how everything works.

| Parameter  | What it adjusts                                                      | Range | Default value |
| ---------- | -------------------------------------------------------------------- | ----- | ------------- |
| `voice`    | Preset number: 0 is user-defined; 1-5 are randomly generated presets | ???   |               |
| `lfofreq`  | Overall pitch modulation frequency                                   | ???   |               |
| `lfodepth` | Overall pitch modulation amplitude                                   | ???   |               |

Each operator (`<op>` 1...6) responds to:

| Parameter         | What it adjusts                                                                       | Range | Default value |
| ----------------- | ------------------------------------------------------------------------------------- | ----- | ------------- |
| `amp<op>`         | Operator `<op>`'s volume - becomes carrier                                            | ???   |               |
| `ratio<op>`       | Frequency ratio of `<op>`                                                             | ???   |               |
| `mod<op><modOp>`  | How much operator `<modOp>` should modulate `<op>` (for feedback, use the same index) | ???
| `detune<op>`      | Detune amount of `<op>` in Hz                                                         | ???   |               |
| `eglevel<op><eg>` | Level of envelope generator `<eg>`                                                    | ???   |               |
| `egrate<op><eg>`  | Rate of envelope generator `<eg>`                                                     | ???   |               |

Examples:

| Setting         | What it adjusts                    |
| --------------- | ---------------------------------- |
| `amp1 1`        | Sets op1 as carrier to full volume |
| `ratio2 2.3`    | Sets op2 frequency ratio           |
| `mod11 0.5`     | Sets op1 feedback                  |
| `mod12 0.78`    | Sets op1 modulation amount by op2  |
| `detune1 0.2`   | Sets op1 detune                    |
| `eglevel12 0.1` | Sets EG2's level on op1            |
| `egrate11 0.01` | Sets EG1's rate on op1             |

:::warning
Higher values go FASTER!
:::

## Drum synthesis
#### Superhex

Waveguide mesh, hexagonal drum-like membrane:

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `rate`       | ??                 | ???   | 1             |
| `accelerate` | Pitch glide amount | ???   | 0             |

### Superkick

Kick Drum using [Rumble-San](http://blog.rumblesan.com/post/53271713518/drum-sounds-in-supercollider-part-1)’s implementation as a starting point:

| Parameter    | What it adjusts                                  | Range | Default value |
| ------------ | ------------------------------------------------ | ----- | ------------- |
| `n`          | Kick frequency in a nonstandard way              | ???   |               |
| `accelerate` | Sweep on the click filter frequency              | ???   | 0             |
| `pitch1`     | Click frequency                                  | ???   | 1             |
| `decay`      | Click duration relative to the overall timescale | ???   | 1             |

### Super808

A vaguely 808-ish kick drum:

| Parameter | What it adjusts    | Range | Default value |
| --------- | ------------------ | ----- | ------------- |
| `n`       | Chirp frequency    | ???   |               |
| `rate`    | Filter sweep speed | ???   | 1             |
| `voice`   | Sinewave feedback  | ???   | 0             |

### Superhat

Hi-hat using [Rumble-San](http://blog.rumblesan.com/post/53271713518/drum-sounds-in-supercollider-part-1)’s implementation as a starting point:

| Parameter    | What it adjusts                           | Range | Default value |
| ------------ | ----------------------------------------- | ----- | ------------- |
| `n`          | Variation on the frequency in a weird way | ???   |               |
| `accelerate` | Sweep on filter                           | ???   | 0             |

### Supersnare

Snare drum using [Rumble-San](http://blog.rumblesan.com/post/53271713518/drum-sounds-in-supercollider-part-1)’s implementation as a starting point:

| Parameter    | What it adjusts                               | Range | Default value |
| ------------ | --------------------------------------------- | ----- | ------------- |
| `n`          | Variation on frequency                        | ???   |               |
| `decay`      | Scaling noise duration relative to tonal part | ???   | 1             |
| `accelerate` | Tonal glide                                   | ???   | 0             |

### Superclap

Hand clap using [Rumble-San](http://blog.rumblesan.com/post/53271713518/drum-sounds-in-supercollider-part-1)’s implementation as a starting point:

| Parameter | What it adjusts          | Range | Default value |
| --------- | ------------------------ | ----- | ------------- |
| `n`       | How spread is calculated | ???   | ???           |
| `delay`   | Echo delay               | ???   | 1             |
| `rate`    | Decay time               | ???   | 1             |
| `pitch1`  | Bandpass frequency       | ???   | 1             |

### SOSKick

Kick drum synth. Increase `pitch1` and `voice` for interesting electronic percussion:

| Parameter | What it adjusts                   | Range                   | Default value |
| --------- | --------------------------------- | ----------------------- | ------------- |
| `pitch1`  | Modulation frequency in Hz        | 0 - `SampleRate.ir / 2` | 0             |
| `voice`   | Modulation input phase in radians | 0 - your sanity         | 1             |
| `pitch2`  | White noise amplitude             | 0 - 1                   | 0             |
| `speed`   | White noise sweep                 | 0 - 1                   | 0.3           |
| `freq`    | ???                               | ???                     | 65            |

### SOSHats

| Parameter   | What it adjusts                  | Range                   | Default value |
| ----------- | -------------------------------- | ----------------------- | ------------- |
| `resonance` | Bandpass filter resonance value  | 0 - 1                   | 1             |
| `pitch1`    | Oscillator modulation in radians | 0 - `SampleRate.ir / 2` | 238.5         |
| `sustain`   | Sustain amount                   | ???                     | 0.5           |
| `freq`      | Frequency                        | ???                     | 220           |

### SOSToms

| Parameter | What it adjusts                   | Range           | Default value |
| --------- | --------------------------------- | --------------- | ------------- |
| `voice`   | Modulation input phase in radians | 0 - your sanity | 0.5           |
| `sustain` | Sustain amount                    | ???             | 0.5           |
| `freq`    | Frequency                         | ???             | 261.626       |

### SOSSnare

| Parameter   | What it adjusts                                  | Range           | Default value |
| ----------- | ------------------------------------------------ | --------------- | ------------- |
| `voice`     | Modulation input phase in radians                | 0 - your sanity | 0.385         |
| `semitone`  | Modulation frequency in semitones of fundamental | ???             | 0.452         |
| `pitch1`    | Resonance filter frequency (Hz)                  | ???             | 2000          |
| `resonance` | Resonance of bandpass and resonz filters         | 0 - 1           | 0.1           |
| `freq`      | Frequency                                        | ???             | 405           |

## Audio Input 
### Live audio input - `in`

| Parameter | What it adjusts | Range | Default value |
| --------- | --------------- | ----- | ------------- |
| `in`      | Audio input     | ???   |               |

### Pitch shifted live audio input - `inr`

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `inr`        | Audio input        | ???   |               |
| `accelerate` | Pitch glide amount | ???   | 0             |

## Other synths and goodies 

### Modulated band limited impulse - `imp`

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |

### Modulated phase mod sines - `psin`

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |

### Gabor grain - `gabor`

???

### Shepard on a cycle - `cyclo`

| Parameter    | What it adjusts    | Range | Default value |
| ------------ | ------------------ | ----- | ------------- |
| `accelerate` | Pitch glide amount | ???   | 0             |

### Synth siren - Supersiren

A controllable synth siren, defaults to 1 second, draw it out with `sustain`.

### Supergrind

From `synthdef.art` fragment (2018-08-16):

| Parameter    | What it adjusts                                                       | Range | Default value |
| ------------ | --------------------------------------------------------------------- | ----- | ------------- |
| `accelerate` | Pitch glide amount                                                    | ???   | 0             |
| `detune`     | Oscillator detune (in Hz, but even small values are quite noticeable) | ???   | 0             |
| `voice`      | Changes harmonics                                                     | ???   | 0             |
| `rate`       | Impulse trigger rate                                                  | ???   | 1             |