---
layout: page
title: Documentation
permalink: /docs/
---

<!--COSMO is based on our COSMO-HAT circuit. The C-HAT allows to connect up to 8 analog control inputs (sensors, expression pedals etc.), as well as an array of 8 LEDs. The C-HAT furthermore, supports a MIDI-In and MIDI-Out connection, which makes the COSMO device more flexible for applications like a standalone Csound based synthesizer or for interactive sound installations.-->




Required Preparation Steps:
- 1. Soldering the Power Converter from 9V to 5V (one for each box)
- 2. Soldering OpAmps on the Cross Mixer Board (2 for each box)
- 3. Soldering Cables to a) Jack Sockets; b) Potentiometers; c) Stomp Switches (approx 4-5 each per box)
- 4. Soldering Cables to Mini-Jack/Chinch connectors (2x for each box) and Dry/Wet Potentiometer
- 5. Finalize Cross Mixer Boards, by attaching to each: Jack-In/Out; (4x) Mini-Jack(or Chinch) I/O (2x); Dry/Wet Potentiometer (1x), True Bypass FootSwitch (1x)
- 6. Soldering Cosmo Plank connection to a) GPIO header (of RPI for Wooden Design) or b) to Extension Pins of Cirrus Logic Card (for Metal Box Design)


More instructions coming soon..

### Building instructions

## 1. Power Supply Unit
- Solder 9V connector to the In (- ground; +) of the MH-MINI-360 converter
![alt text](/images/instructions/1_VoltageConverter.png)
- Negative is center on guitar equipment!
- connect 9V power supply to the connector
- Use a voltmeter to test from the out(-) of the converter circuit to the input, you should see the 9V
- measure the output of the converter, which will be 9V or lower
- use a screwdriver to adjust the screw on the circuit until you measure 5V output
![alt text](/images/instructions/2b_VoltageConverterAdjust.png)
- solder the red (+) and the black (-) leads of a micro USB-cable to the output of the converter.
![alt text](/images/instructions/2_VoltageConverterCable.png)


## 2. Setting up the Raspberry Pi
- Copy our [Raspian Image]((https://drive.google.com/file/d/0B-Iu7KEexnCpOTk2N0RoY2hiaHM/view?usp=sharing) to a 8GB micro SD card 
- Connect the micro USB from the power converter cable to the Raspberry Pi 3 (RPI), it should boot up
- Connect the RPI to your computer via Ethernet connection
- Open the terminal/console on your mac or linux computer (Windows users should use [Putty](http://www.putty.org/)) 
- Login: "ssh pi@cosmo1.local" (if "cosmo1.local" doesn't work, try pinging "cosmo1.local" to get the IP address and then use the same command, but with IP address instead of "cosmo1.local") 
- Password: raspberry
- Test csound: "cd cosmo-dsp/WorkshopTestFiles/"
- Run: "csound audio-out-test.csd"
- Press Ctrl+C to stop Csound
- Run: "logout"
- Turn off the RPI by unplugging the mini usb power

## 3. Drill holes into the enclosure

- Measures of holes to drill for components

* Stomp Switch : 12mm 
![alt text](/images/instructions/components/stomp_switch.jpg width="150")
* Stereo Potentiometer : 7mm
![alt text](/images/instructions/components/stereo_pot.jpg)
* Mono Potentiometer : 7mm
![alt text](/images/instructions/components/pot.jpg)
* 5mm LED : 8mm
![alt text](/images/instructions/components/led_5mm.jpg)
* Toggle Switch : 6mm
![alt text](/images/instructions/components/toggle_switch.jpg)
* Small Push Button : 7mm
![alt text](/images/instructions/components/small_push_button.jpg)
* 6.35mm Jack (in/out)  : 9mm
![alt text](/images/instructions/components/jack_635mm.jpg)

## 4. Test COSMO plank

- Coming...

## 5. Fit everything into the enclosure
- Mount knobs and switches
- Solder connections to the COSMO plank
- Connect USB-Soundcard or Cirrus Audio Logic HAT to RPI
- Connect Soundcard In- and Outputs to Jack connectors in the enclosure


## 6. Crossmixer Board
- Coming...


## <a name="csound"></a>Basic Csound on COSMO

On the COSMO box, we use a python script to hanlde both Csound and the data from the microcontroller (switches, leds and knobs). This script is called **cosmo.py** and resides within the [cosmohat-fw](https://github.com/cosmoproject/cosmohat-fw)-repository. On our Raspbian image, this python file is called from the script **startup.sh**, which runs when the COSMO boots, so this is where you change which Csound file (has the ending _.csd_) you want to use. To change the csd file, you need to change the variable called **csoundFile** in **startup.sh** which has a string that points to a specific csd file:

```

csoundFile = "/home/pi/cosmo-dsp/WorkshopTestFiles/knob-test.csd"

```

As the path indicates, the Csound files are placed in a separate folder which is a clone of the [cosmo-dsp](https://github.com/cosmoproject/cosmo-dsp)-repository. At the moment we have to folders:

- **WorkshopTestFiles:**
        This folder contains some simple test files to test audio in/out, switches, leds and knobs (file names are quite self explanatory). There is also a basic synthesizer example where you can use the switches to turn on and off different oscillators and use the knobs to control their individual frequencies. 

- **Effects:**
        We have tried to make a as simple as possible solution for those unfamiliar with Csound to be able to patch different effects together. The separate effects are placed in the folder called **UDOs** (UDO stands for User Defined Opcode) and the file **SimpleSetup.csd** shows the basics to combine the effects and map the controllers onto the effect parameters:

```
#include "UDOs/Reverb.csd"
#include "UDOs/Lowpass.csd"
```

Since the Csound code is placed in separate files, we need these lines to include the actual code for Reverb and Lowpass. If you want to use e.g. the MultiDelay effect you need to add the line **#include "UDOs/MultiDelay.csd"**

```
instr 1 
#include "includes/adc_channels.inc"
#include "includes/gpio_channels.inc"
#include "includes/switch2led.inc"
```

The two first files includes the code for reading the knobs, switches and leds. The values from these are put into global control rate variables called **gkpotX**, **gkswitchX** and **gkledX** accordingly (the X represents the number (0-indexed) of the controller, so the first knob would get the name **gkpot0** 

The file **switch2led.inc** includes code which connects led 1 to switch 1 etc. If you want to control the leds directly, you need to remove this include line.

```
aL, aR ins
```

This is the code for getting audio into Csound. **ins** is a Csound opcode (a native Csound module) which ouputs the incoming audio into the audio rate variables **aL** and **aR**


```
; Reverb arguments: decay, cutoff, mix
aL, aR Reverb aL, aR, gkpot0, gkpot1, gkswitch0

```

Reverb is a UDO (User Defined Opcode) which takes a stereo input signal with 3 arguments (decay, cutoff and mix) and applies reverberation to the signal. The ouput is also a stereo signal. Notice that **aL** and **aR** are used on both right and left side of **Reverb**; this means that we first send the dry signal into the reverb effect and then overwrite the dry signal with the reverberant signal. This way makes it very easy to switch the order of effects without changing any code - you simply just reorder by switching lines.

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

This example was made to be as simple and clear as possible. To see a bit more advanced example which illustrates how you can achieve more flexible routing like sending to different effects in parallell, see the files **ExampleSetup.csd**. 

A basic understanding of Csound is highly recommended before getting too experimental. The FLOSS manual is an excellent resource for learning Csound: 

[http://floss.booktype.pro/csound/preface/](http://floss.booktype.pro/csound/preface/)




