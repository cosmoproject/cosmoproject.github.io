---
layout: page
title: DSP Library
permalink: /dsp/
---

### DSP Library
A basic collection of DSP code for the COSMO can be found in this [repository](https://github.com/cosmoproject/cosmo-dsp).

This repository comprises a library with [Audio Effects] (https://github.com/cosmoproject/cosmo-dsp/tree/master/DSP-Library/Effects) (e.g Reverbs, Delays, Distortion ..). If you have experience in writing Csound Patches, you can take one of the [examples] (https://github.com/cosmoproject/cosmo-dsp/tree/master/Examples) and modify them.

A better way to start building your effect instrument is using the [COSMO-Patcher] (https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher). Here you can define your instrument by simply assigning effect parameters to the harware controllers. A simple Patch looks like this:

    {"COSMO-Patch": {
        "pot0":
            {
                "Reverb": "Decay time",
                "Lowpass": "Cutoff frequency"
            },
        "pot1":
            {
                "Reverse": "Dry/wet mix"
            }
        }
    }
    
From this structure, the 'JsonToCsd.py' converter can generate the according Csound file. Find more instructions [here] (https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher).


![alt text](/images/Live_01.png "Live-01")

## List of supported effect UDOs: 
| UDO              | Arguments                                                                                                                                    |
|:-----------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| AnalogDelay.csd  | Delay time, Feedback, Dry/wet mix                                                                                                            |
| Blur.csd         | Blur time, Gain, StereoMode, Dry/wet mix                                                                                                     |
| Chorus.csd       | Feedback, Dry/wet mix                                                                                                                        |
| Distortion.csd   | Level, Drive, Tone, Dry/wet mix                                                                                                              |
| FakeGrainer.csd  | Dry/wet mix                                                                                                                                  |
| Hack.csd         | Frequency, Dry/wet mix                                                                                                                       |
| Lowpass.csd      | Cutoff frequency, Resonance, Distortion                                                                                                      |
| MultiDelay.csd   | Multi tap on/off, Delay time, Feedback, Cutoff, Dry/wet mix                                                                                  |
| PitchShifter.csd | Semitones (-/+ 1 octave), Stereo mode, Dry/wet mix                                                                                           |
| RandDelay.csd    | Range, Feedback, Dry/wet mix                                                                                                                 |
| Repeater.csd     | Range, Repeat time, On/off                                                                                                                   |
| Reverb.csd       | Decay time, Cutoff frequency, Dry/wet mix                                                                                                    |
| Reverse.csd      | Reverse time, Dry/wet mix                                                                                                                    |
| SimpleLooper.csd | Record/Play, Stop/start, Speed, Reverse, Audio Through                                                                                       |
| SineDelay.csd    | Range, Frequency, Feedback, Dry/wet mix                                                                                                      |
| SolinaChorus.csd | LFO1 Frequency, LFO1 Amp, LFO2 Frequency, LFO2 Amp, Stereo mode on/off, Dry/wet mix                                                          |
| Tremolo.csd      | Frequency, Depth                                                                                                                             |
| TriggerDelay.csd | Threshold, DelayTime Min, DelayTime Max, Feedback Min, Feedback Max, Width, Level, Portamento time, Cutoff frequency, Bandwidth, Dry/wet mix |
| Volume.csd       | Level                                                                                                                                        |
| Wobble.csd       | Frequency, Dry/wet mix                                                                                                                       |

## Note

 We are planning to build a community sharing their individual csound-based effect instruments. If you'd like to share your code, [contact us](mailto:csoundonstage@gmail.com) and become added to the git-repository.
