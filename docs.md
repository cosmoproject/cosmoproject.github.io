---
layout: page
title: Documentation
permalink: /docs/
---

COSMO is based on our COSMO-HAT circuit. The C-HAT allows to connect up to 8 analog control inputs (sensors, expression pedals etc.), as well as an array of 8 LEDs. The C-HAT furthermore, supports a MIDI-In and MIDI-Out connection, which makes the COSMO device more flexible for applications like a standalone Csound based synthesizer or for interactive sound installations.

![alt text](/images/COSMO-HAT.jpg "COSMO hat")

More instructions coming soon..

### Building instructions

##1. Power Supply Unit
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


##2. Setting up the Raspberry Pi
- copy our (insert LINK here!) Raspian Image to a 4GB micro SD card
- connect the micro USB from the power converter cable to the Raspberry Pi 2 (RPI), it should boot up
- connect the RPI to your computer via Ethernet connection
- open the terminal/console on your mac or linux computer
- find the RPI network adress: "arp -an" 
- login: "ssh pi@169.254.38.74" (ssh pi@raspberrypi.local)
- pw: raspberry
- test csound: "cd cosmo-dsp/WorkshopTestFiles/"
- run: "csound audio-out-test.csd"
- press Cmd+C to stop Csound
- run: "logout"
- turn off the RPI by unplugging the mini usb power

##3. Prepare the COSMO-HAT 
![alt text](/images/instructions/3_COSMORaw.jpg)

- solder the 40 Pin connector to the COSMO Hat
- solder the rainbow cable to the analog input channels (brown = 0)
- solder the rainbow cable to the digital input/output channels (brown = 0)
- solder middle of potentiometers to analog ins, or tip of jack connectors



##4. Setup RPI with COSMO-HAT
- attach the COSMO Hat to the RPI (no power!)
- log into RPI using SSH (Step 2)
- run: ~/cosmohat-fw $ make fuse

##5. Drill holes into the enclosure

- Measures of holes to drill for components
Stompswitch = 12mm
MainStereoPotentiometer = 8mm
LED = 8mm
SwitchOnOff = 4mm
JackInOut = 10mm

##6. Prepare USB and Ethernet connections


##7. Fit everything into the enclosure
- Mount knobs and switches
- solder connections to the COSMO-Hat (Photo with description of Pins, Middle = AD, Left = GND, Right = 3.3V)
- Connect USB-Soundcard to RPI
- Connect Soundcard In- and Outputs to Jack connectors in the enclosure


##8. Crossmixer Board
- Future..


## <a name="csound"></a>Basic Csound on COSMO

On the COSMO box, we use a python script to hanlde both Csound and the data from the microcontroller (switches, leds and knobs). For the time being this script is called "csndPython\_SPI\_test.py" and resides within the [cosmohat-fw](https://github.com/cosmoproject/cosmohat-fw)-repository. This python file runs when the COSMO boots and is where you change which Csound file (has the ending "csd") you want to use. To change the csd file, you need to change the variable called "csoundFile" (at the beginning of the python script) which has a string that points to a specific csd file:

```

csoundFile = "/home/pi/cosmo-dsp/WorkshopTestFiles/knob-test.csd"

```

As the path indicates, the Csound files are placed in a separate folder which is a clone of the [cosmo-dsp](https://github.com/cosmoproject/cosmo-dsp)-repository. At the moment we have to folders:

- WorkshopTestFiles
        This folder contains some simple test files to test audio in/out, switches, leds and knobs (file names are quite self explanatory). There is also a basic synthesizer example where you can use the switches to turn on and off different oscillators and use the knobs to control their individual frequencies. 

- Effects
        We have tried to make a as simple as possible solution for those unfamiliar with Csound to be able to patch different effects together. The separate effects are placed in the folder called "UDOs" (UDO stands for User Defined Opcode) and the file "SimpleSetup.csd" shows the basics to combine the effects and map the controllers onto the effect parameters:

```
#include "UDOs/Reverb.csd"
#include "UDOs/Lowpass.csd"
```

Since the Csound code is placed in separate files, we need these lines to include the actual code for Reverb and Lowpass. If you want to use e.g. the MultiDelay effect you need to add the line "#include "UDOs/MultiDelay.csd"

```
instr 1 
#include "includes/adc_channels.inc"
#include "includes/gpio_channels.inc"
#include "includes/switch2led.inc"
```

The two first files includes the code for reading the knobs, switches and leds. The values from these are put into global control rate variables called "gkpotX", "gkswitchX" and "gkledX" accordingly (the X represents the number (0-indexed) of the controller, so the first knob would get the name "gkpot0" 

"switch2led.inc" includes codes which connects led1 to switch1 etc. If you want to control the leds directly, you need to remove this include line.

```
aL, aR ins
```

This is the code for getting audio into Csound. "ins" is a Csound opcode (a native Csound module) which ouputs the incoming audio into the audio rate variables "aL" and "aR"


```
; Reverb arguments: decay, cutoff, mix
aL, aR Reverb aL, aR, gkpot0, gkpot1, gkswitch0

```

Reverb is a UDO (User Defined Opcode) which takes a stereo input signal with 3 arguments (decay, cutoff and mix) and applies reverberation to the signal. The ouput is also a stereo signal. Notice that "aL" and "aR" are used on both right and left side of "Reverb"; this means that we first send the dry signal into the reverb effect and then overwrite the dry signal with the reverberant signal. This way makes it very easy to switch the order of effects without changing any code - you simply just reorder by switching lines.

The arguments are where set up how you use your knobs and switches to control the different effects. In this example the two first knobs will control the decay time and lowpass filter cutoff, while the first switch will turn the effect on and off (by sending 0 or 1 to the mix argument). All scaling are done inside the effects, so all input arguments should be normalized (0 to 1). 
    
```
; Lowpass_Stereo arguments: cutoff, resonance
aL, aR Lowpass_Stereo aL, aR, gkpot2, gkpot3
```

Here a stereo lowpass filter is applied to the signal coming out from the Reverb effect. Knob 3 and 4 are set up to control the filter cutoff and resonance respectively. The lowpass filter also have a distortion argument which we don't use here. All effects are made in this way so actually all arguments are optional, but only in the order they are placed (e.g. you can't skip resonance and then include distortion). 

```
outs aL, aR
```
The audio coming out from the lowpass filter are sent to the "outs" opcode which sends the audio to the actual hardware device (sound card).

This example was made to be as simple and clear as possible. To see a bit more advanced example which illustrates how you can achieve more flexible routing like sending to different effects in parallell, see the files "ExampleSetup.csd". 

A basic understanding of Csound is highly recommended before getting too experimental. The FLOSS manual is an excellent resource for learning Csound: [http://floss.booktype.pro/csound/preface/](http://floss.booktype.pro/csound/preface/)





