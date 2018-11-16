---
layout: page
title: Programming COSMO
permalink: /dsp/
---

A basic collection of DSP code for the COSMO can be found in this github repository: [https://github.com/cosmoproject/cosmo-dsp](https://github.com/cosmoproject/cosmo-dsp). An overview and quick explanation of the repository structure can be found [below](#dsp-lib-structure)

This repository comprises a library of ready-made [audio effects](https://github.com/cosmoproject/cosmo-dsp/tree/master/DSP-Library/Effects) (e.g Reverb, Delay, Distortion ..). All effects are set up as independendant modules that can be combined to a custom setup of effects. There are two ways of using this library to program your COSMO. You can either [program your own Csound patches](#BasicCsoundOnCOSMO) or use our toolset [COSMO Patcher](#COSMO-Patcher)


If you have experience in writing Csound patches, you can take one of the [examples](https://github.com/cosmoproject/cosmo-dsp/tree/master/Examples) and modify them.

**Table of contents**

* TOC
{:toc}


## 1. COSMO Patcher

A better way to start building your effect instrument is using the [COSMO-Patcher](https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher). With this you can define your instrument by simply assigning 'effect arguments' (see List of supported effect UDOs) to the harware controllers. A simple patch looks like this:

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
    
From this structure, the 'JsonToCsd.py' converter can generate the according Csound file. Find more instructions [here](https://github.com/cosmoproject/cosmo-dsp/tree/master/COSMO-Patcher). If you're using the COSMO image, you don't need to do the install part. 



### 1.1 List of supported audio effects:

## List of effects: 
| Effect              | Arguments |
|:-----------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| Blur.udo         | Blur time, Gain, Dry/wet mix[, StereoMode]                                                                                                   |
| Chorus.udo       | Feedback, Dry/wet mix                                                                                                                        |
| Distortion.udo   | Level, Drive, Tone, Dry/wet mix                                                                                                              |
| FakeGrainer.udo  | Dry/wet mix                                                                                                                                  |
| Hack.udo         | Frequency, Dry/wet mix                                                                                                                       |
| Highpass.udo     | Cutoff_frequency, Resonance, Distortion [, Mode]                                                                                             |
| Lowpass.udo      | Cutoff frequency, Resonance, Distortion [, Mode]                                                                                             |
| RandDelay.udo    | Range, Speed, Feedback, Dry/wet mix, [Stereo Mode 1i/1o only]                                                                                |
| Reverb.udo       | DecayTime, HighFreq_Cutoff, DryWet_Mix, Mode                                                                                                 |
| Reverse.udo      | Reverse_time, Speed, Dry/wet mix                                                                                                             |
| SineDelay.udo    | Range, Frequency, ModulationIdx, Feedback, Dry/wet mix                                                                                       |
| TapeDelay.udo    | DelayTime, Feedback, Filter, Mix [, StereoMode]                                                                                              |
| Tremolo.udo      | Frequency, Depth, Dry/wet mix [, StereoMode]                                                                                                 |
| TriggerDelay.udo | Threshold, DelayTime Min, DelayTime Max, Feedback Min, Feedback Max, Width, Level, Portamento time, Cutoff frequency, Bandwidth, Dry/wet mix |
| Volume.udo       | Level                                                                                                                                        |
| Wobble.udo       | Frequency, Dry/wet mix                      |

<!--
| Effect              | Arguments |
| -----------------| :---------------------------------------------------------------------------------------------------------------------------------------------|
| [AnalogDelay.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/AnalogDelay.udo)  | Delay time, Feedback, Dry/wet mix                                                                                                            |
| [Blur.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Blur.udo) | Blur time, Gain, StereoMode, Dry/wet mix                                                                                                     |
| [Chorus.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Chorus.udo)       | Feedback, Dry/wet mix                                                                                                                        |
| [Distortion.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Distortion.udo)   | Level, Drive, Tone, Dry/wet mix                                                                                                              |
| [FakeGrainer.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/FakeGrainer.udo)  | Dry/wet mix                                                                                                                                  |
| [Hack.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Hack.udo)         | Frequency, Dry/wet mix                                                                                                                       |
| [Lowpass.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Lowpass.udo)      | Cutoff frequency, Resonance, Distortion                                                                                                      |
| [MultiDelay.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/MultiDelay.udo)   | Multi tap on/off, Delay time, Feedback, Cutoff, Dry/wet mix                                                                                  |
| [PitchShifter.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/PitchShifter.udo) | Semitones (-/+ 1 octave), Stereo mode, Dry/wet mix                                                                                           |
| [RandDelay.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/RandDelay.udo)    | Range, Feedback, Dry/wet mix                                                                                                                 |
| [Repeater.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Repeater.udo)     | Range, Repeat time, On/off                                                                                                                   |
| [Reverb.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Reverb.udo)       | Decay time, Cutoff frequency, Dry/wet mix                                                                                                    |
| [Reverse.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Reverse.udo)      | Reverse time, Dry/wet mix                                                                                                                    |
| [SimpleLooper.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/SimpleLooper.udo) | Record/Play, Stop/start, Speed, Reverse, Audio Through                                                                                       |
| [SineDelay.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/SineDelay.udo)    | Range, Frequency, Feedback, Dry/wet mix                                                                                                      |
| [SolinaChorus.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/SolinaChorus.udo) | LFO1 Frequency, LFO1 Amp, LFO2 Frequency, LFO2 Amp, Stereo mode on/off, Dry/wet mix                                                          |
| [Tremolo.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Tremolo.udo)      | Frequency, Depth                                                                                                                             |
| [TriggerDelay.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/TriggerDelay.udo) | Threshold, DelayTime Min, DelayTime Max, Feedback Min, Feedback Max, Width, Level, Portamento time, Cutoff frequency, Bandwidth, Dry/wet mix |
| [Volume.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Volume.udo)       | Level                                                                                                                                        |
| [Wobble.udo](https://github.com/cosmoproject/cosmo-dsp/blob/master/DSP-Library/Effects/Wobble.udo)       | Frequency, Dry/wet mix |
-->

## 2. Basic Csound on COSMO

This section will give you a quick overview of how to program your own basic Csound patches for the COSMO. If you already have experience in writing Csound patches, you can have a looke at one of our [examples](https://github.com/cosmoproject/cosmo-dsp/tree/master/Examples) and modify them.

On the COSMO box, we use a python script to handle both Csound and the data from the microcontroller (switches, leds and knobs). This script is called **```cosmo.py```** and resides within the [cosmo-fw](https://github.com/cosmoproject/cosmo-fw)-repository. On our Raspbian image, this python file is called from the script **```startup.sh```**, which runs when the COSMO boots, so this is where you change which Csound file (has the ending _.csd_) you want to use. To change the csd file, you need to change the variable called **```csoundFile```** in **```startup.sh```** which has a string that points to a specific csd file:

```

csoundFile = "/home/pi/cosmo-dsp/WorkshopTestFiles/knob-test.csd"

```

**IMPORTANT!**<br>

The folder **```cosmo-dsp```** is a [git repository](https://en.wikipedia.org/wiki/Git), which means that you should NOT edit any files within this folder if you want to be able to update the DSP library without too much hassle at a later point. You should therefor keep your own Csound files in a local folder in your home folder: **```/home/pi```**. You can use the command **```pwd```** to check which folder you're currently in.

**Tip!** *You can press the tab key to autocomplete folder and file names when typing in terminal*

<a name="make-local-copy"></a>
To make a new folder that can keep your own local Csound files, you can use these commands: 

```
$ cd /home/pi
$ mkdir csound
``` 
This will make a new folder called **```csound```**, but you can use any name you want by changing the argument after **```mkdir```**

If you want to use one of the examples as a starting point, you can use these commands to make a local copy called **```MyEffectSetup.csd```**:

```
$ cd /home/pi
$ cp cosmo-dsp/Examples/SimpleEffectSetup.csd csound/MyEffectSetup.csd
```

Since the include paths used in all the examples file are relative to their placement within the **```cosmo-dsp```**-folder, they need to be updated to work from the new location. To edit you're newly created local copy, use these commands:

```
$ cd /home/pi/csound
$ nano MyEffectSetup.csd
``` 
Now replace all instances of **```../DSP-Library```** with **```../cosmo-dsp/DSP-Library```**

Remember that you need to change the **```csoundFile```**-variable in **```startup.sh```** to point to **```/home/pi/csound/MyEffectSetup.csd```** to make this the Csound file that runs at startup.

### 2.1 **```cosmo-dsp```** directory structure

As the path indicates, the Csound files are placed in a separate folder which is a clone of the [cosmo-dsp](https://github.com/cosmoproject/cosmo-dsp)-repository. At the moment this repository have the following structure:


- **```/COSMO-Patcher```**

    This folder contains the [COSMO Patcher toolset](#1-cosmo-patcher) explained above.

- **```/Examples```**

    Some simple example files that show how to use the COSMO DSP library without using the [COSMO Patcher toolset](#1-cosmo-patcher).

- **```/WorkshopTestFiles```**

    This folder contains some simple test files to test audio in/out, switches, leds and knobs (file names are quite self explanatory). There is also a basic synthesizer example where you can use the switches to turn on and off different oscillators and use the knobs to control their individual frequencies. 

- **```/DSP-Library```**

    We have tried to make a solution as simple as possible for those unfamiliar with Csound to be able to patch different effects and instruments together. All the effects and instruments are placed in separate files and embedded in something called a **UDO** (UDO stands for User Defined Opcode) with normalized input arguments (0-1) for the effect control parameters. Proper scaling are done inside the UDO and the actual parameter ranges can be found in the header of each effect and instrument file.   

    - **```/Cabbage```**

        A selection of the effects from the **```/Effects```**-folder reworked as Cabbage ([http://http://cabbageaudio.com/](http://cabbageaudio.com/)) plugins.


    - **```/Effects```**            

        A selection of basic (and some a bit more advanced) effects written in Csound as UDOs. Check out the file **```SimpleEffectSetup.csd```** in the **```/Examples```**-folder for an example of how to put these effect modules together.  

    - **```/Instruments```**

        A few very basic instruments written in Csound as UDOs. Very much work in progress yet. Check out the file **```SimpleInstrumentSetup.csd```** in the **```/Examples```**-folder for an example of how to put these instrument modules together.  


    - **```/Includes```**

        Some files to be included in your Csound code to add support for MIDI input (**```all_midi_cc.inc```**), COSMO plank/HAT switches and leds (**```gpio_channels.inc```**) and COSMO plank/HAT pots (**```adc_channels.inc```**). Also a file (**```cosmo_utilities.inc```**) with some utility functions used by several effect UDOs, that needs to be included in your Csound orchestera (see **```SimpleEffectSetup.csd```** in the **```/Examples```**-folder for an example)

    - **```/SoundFiles```**

        Some sound files that can be used for e.g. granular synthesis, convolution 

### 2.2 **```SimpleEffectSetup.csd```** explained 

```
#include "../DSP-Library/Includes/cosmo_utilities.inc"
```
This line includes some utility code used by several of the effects and instruments and should always be included first when using the **```cosmo-dsp```**-library

```
#include "../DSP-Library/Effects/Reverb.csd"
#include "../DSP-Library/Effects/Lowpass.csd"
```

Since the Csound code is placed in separate files, we need these lines to include the actual code for Reverb and Lowpass. If we wanted to use e.g. the TapeDelay effect we would need to add the line **```#include "../DSP-Library/Effects/TapeDelay.csd"```**. 

**IMPORTANT!** The paths used in the example is based on the placement of the example files within the **```cosmo-dsp```** directory structure. If you want to modify this example instead of starting from scratch, see start of section [2. Basic Csound on COSMO](#2-basic-csound-on-cosmo) for explanation of how to make a local copy and do the necessesary modifications.

```
instr 1 
    #include "../DSP-Library/Includes/adc_channels.inc"
    #include "../DSP-Library/Includes/gpio_channels.inc"
```

The two first files includes the code for reading the knobs, switches and leds. The values from these are put into global control rate variables called **gkpotX**, **gkswitchX** and **gkledX** accordingly (the X represents the number (0-indexed) of the controller, so the first knob would get the name **gkpot0** 

```
aL, aR ins
```

This is the code for getting audio into Csound. **```ins```** is a Csound opcode (a native Csound module) which ouputs the incoming audio into the audio rate variables **```aL```** and **```aR```**


```
; Reverb arguments: decay, cutoff, mix
aL, aR Reverb aL, aR, gkpot0, gkpot1, gkswitch0

```

Reverb is a UDO (User Defined Opcode) which takes a stereo input signal with 3 arguments (decay, cutoff and mix) and applies reverberation to the signal. The ouput is also a stereo signal. Notice that **```aL```** and **```aR```** are used on both right and left side of **```Reverb```**; this means that we first send the dry signal into the reverb effect and then overwrite the dry signal with the reverberant signal. This way makes it very easy to switch the order of effects without changing any code - you simply just reorder by switching lines.

The arguments are where set up how you use your knobs and switches to control the different effects. In this example the two first knobs will control the decay time and lowpass filter cutoff, while the first switch will turn the effect on and off (by sending 0 or 1 to the mix argument). All scaling are done inside the effects, so all input arguments should be normalized (0 to 1). 
    
```
; Lowpass_Stereo arguments: cutoff, resonance
aL, aR Lowpass_Stereo aL, aR, gkpot2, gkpot3
```

Here a stereo lowpass filter is applied to the signal coming out from the reverb effect. Knob 3 and 4 are set up to control the filter cutoff and resonance respectively. The lowpass filter also have a distortion argument which we don't use here. All effects are made in this way so actually all arguments are optional, but only in the order they are placed (e.g. you can't skip resonance and then include distortion). 

```
outs aL, aR
```
The audio coming out from the lowpass filter are sent to the **outs** opcode which sends the audio to the actual hardware device (sound card).

This example was made to be as simple and clear as possible. 

<!--To see a bit more advanced example which illustrates how you can achieve more flexible routing like sending to different effects in parallell, see the files **ExampleSetup.csd**. -->

A basic understanding of Csound is highly recommended before getting too experimental. The FLOSS manual is an excellent resource for learning Csound: 

[http://floss.booktype.pro/csound/preface/](http://floss.booktype.pro/csound/preface/)


### 2.3 Modify **```SimpleEffectSetup.csd```** for MIDI  

To make the **```SimpleEffectSetup.csd```** work with a MIDI-controller, a few changes needs to be done (*remember to work on your local copy!*). First you need to add the option **```-Ma```** to **```<CsOptions>```** like this:

```
-odac:hw:1,0 -iadc:hw:1 -d -+rtaudio=ALSA -b512 -B2048 -j4 --realtime -Ma
```

Secondly, you need to change the first lines in instrument 1 from this:

```
instr 1 
    #include "../DSP-Library/Includes/adc_channels.inc"
    #include "../DSP-Library/Includes/gpio_channels.inc"
```

to this:

```
instr 1 
    #include "../DSP-Library/Includes/all_midi_cc.inc"

```

Lastly, the format of the variable names have now changed from **```gkpotX```**, **```gkswitchX```** and **```gkledX```** to only being **```gkCHNX_CCY```**, where X is the channel number and Y is the CC number. If you have a MIDI controller with 2 pots on MIDI channel 1 and CC numbers 1 and 2, you can set them to control the cutoff and resonance of the lowpass filter by using this code:

```
; Lowpass_Stereo arguments: cutoff, resonance
aL, aR Lowpass_Stereo aL, aR, gkCHN1_CC1, gkCHN1_CC2
```  

![alt text](/images/Live_01.png "Live-01")

## Contribute

 We want to build a community sharing their individual csound-based effect instruments. If you'd like to share your code, [contact us](mailto:csoundonstage@gmail.com) and become added to the git-repository.
