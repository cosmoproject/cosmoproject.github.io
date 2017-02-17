---
layout: page
title: Documentation
permalink: /docs/
---

<!--COSMO is based on our COSMO-HAT circuit. The C-HAT allows to connect up to 8 analog control inputs (sensors, expression pedals etc.), as well as an array of 8 LEDs. The C-HAT furthermore, supports a MIDI-In and MIDI-Out connection, which makes the COSMO device more flexible for applications like a standalone Csound based synthesizer or for interactive sound installations.-->


<!--
## Required Preparation Steps / First Tasks in Workshop :
- Soldering the Power Converter from 9V to 5V (one for each box) [Alex]
- Soldering OpAmps on the Cross Mixer Board [Kristoffer]
- Soldering Cables to a) Jack Sockets; b) Potentiometers; c) Stomp Switches (approx 4-5 each per box) [Bernt]
- Soldering Cables to Mini-Jack/Chinch connectors (2x for each box) and Dry/Wet Potentiometer
- Finalize Cross Mixer Boards, by attaching to each: Jack-In/Out; (4x) Mini-Jack(or Chinch) I/O (2x); Dry/Wet Potentiometer (1x), True Bypass FootSwitch (1x)
- Soldering Cosmo Plank connection to a) GPIO header (of RPI for Wooden Design) or b) to Extension Pins of Cirrus Logic Card (for Metal Box Design)


More instructions coming soon..
-->

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
- Copy our [Raspian Image](https://drive.google.com/file/d/0B-Iu7KEexnCpOTk2N0RoY2hiaHM/view?usp=sharing) to a 8GB micro SD card 
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
![alt text](/images/instructions/components/stomp_switch.jpg)
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


## <a name="cosmo-software"></a> 

## 1. Setting up and connecting to the Raspberry Pi

	The easiest way of connecting to your Raspberry Pi/COSMO is by connecting both it and your computer to a router or some other existing network. The other solution, which is to set up a direct connection (an ethernet cable) between your computer and RPi/COSMO, involves a few more steps and can have several quirks depending on type and version of OS. 

### 1.1 How to log in to the Raspberry Pi on existing network

	#### OS X
		1. Open Finder, go to "/Applications/Utilities" and open the app called "Terminal"
		2. In the terminal you type "ssh pi@cosmo1.local" ("pi" is the username we use to log on to the Pi and cosmo1.local is the network name for this Pi. If you want a personal network name for your COSMO, see ["How to change the network name of your COSMO](cosmoproject.github.io/docs/#change-network-name))
		3. This should prompt you for a password to log on to the Pi. The default password on the COSMO Raspbian Image is "raspberry"

	#### Windows
		1. Download and install "putty" (www.putty.org/)
		2. Open "putty"
		3. Type in "cosmo1.local" in the "Host name or IP address"-field. Make sure the connection type is set to SSH
		4. Press "Open"
		5. When prompted, type in username "pi" and password "raspberry"


### 1.2 How to log in to the Raspberry Pi using a direct connection 

	#### OS X (names may vary slightly depending on version of OS X)
		1. Connect an Ethernet cable between your computer and Raspberry Pi - make sure the lights on the RPi Ethernet port are lit (orange and green)
		2. On your Mac, press the Apple logo in the top left corner and choose "System Preferences..."
		3. Press the "Sharing" icon
		4. Select the "Internet Sharing" option
		5. In the dropdown menu next to "Share your connection from", select "Wi-Fi"
		6. In the list next to "To computers using" check the box next to "Ethernet" or Thunderbolt Ethernet" (depening on what model your Mac is)
		7. Check the box to the left of "Internet Sharing" (in the column named "On") to start Internet Sharing
		8. You will get a message box displaying a warning - push the "Start" button
		9. Now open Finder and go to "/Applications/Utilities" and open the app called "Terminal"
		10. In the terminal you type "ssh pi@cosmo1.local" ("pi" is the username we use to log on to the Pi and cosmo1.local is the network name for this Pi. If you want a personal network name for your COSMO, see "How to change the network name of your COSMO")
		11. This should prompt you for a password to log on to the Pi. The default password on the COSMO Raspbian Image is "raspberry"
		12. You should now be logged on to your COSMO ready to make some crazy sounds! If you had issues with connecting - see the troubleshooting section

### 1.3 <a name="change-network-name"></a>How to change the network name of your COSMO

	1. Log in to the Raspberry Pi
	2. Run raspi-config
	3. Go to "Advanced ..something"
	4. Go to "Change hostname"
	5. Type in your desired name
	6. Press ok and let the Raspberry reboot
	7. You can now access your Raspberry Pi using the name you chose + '.local' (eg. 'myawesomecosmo.local')


## 2. Testing, calibrating and configuring COSMO

### 2.1 How to test the COSMO plank

	1. Log in to the Raspberry Pi
	2. Kill any running instances of python/csound by typing "killall python" 3 times
	3. Type "cd cosmohat-fw"
	4. Type "python planck.py"
	5. All leds will blink in a binary counting pattern and you will see the values for all pots and switches when you twist and push them
	6. Note down all maximum and minimum values for the analoge inputs


### 2.2 How to configure the COSMO plank or HAT
	
	1. Log in to the Raspberry Pi
	2. Type "nano .cosmo" 
	3. You can now list which inputs are used for switches and which outputs are used for LEDs and change the order
	4. Each analogue input will have two values, min and max, which can be used to calibrate each input (see bullet 6 in section 2.2) and invert the signal (setting max value as min and vica verca) 

How to calibrate the analogue inputs on COSMO plank or COSMO-HAT
	1. Log in to the Raspberry Pi
	2. Type "nano .cosmo"
	3. You can now set minimum and maximum values for all analogue inputs

### 2.3 How to test audio output from Csound

	1. Connect speakers or headphones to the output of the COSMO 
	2. Log in to the Raspberry Pi 
	3. Kill any running instances of python/csound by typing "killall python" 3 times
	4. Type "cd cosmo-dsp"
	5. Type "cd WorkshopTestFiles"
	6. Type "csound audio-out-test.csd"
	7. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
	8. You should now here some decending sine tones coming from the COSMO outputs
	9. Press "Ctrl-C" (possibly twice) to stop Csound

### 2.4 How to test audio input to Csound

	1. Connect an audio source to the input of the COSMO
	2. Connect speakers or headphones to the output of the COSMO 
	3. Log in to the Raspberry Pi 
	4. Kill any running instances of python/csound by typing "killall python" 3 times
	5. Type "cd cosmo-dsp"
	6. Type "cd WorkshopTestFiles"
	7. Type "csound audio-in-test.csd"
	8. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
	9. The audio coming in to the COSMO input should now be passed through Csound and out to the COSMO output. The RMS amplitude value of the input is printed in the console
	10. Press "Ctrl-C" (possibly twice) to stop Csound

### 2.5 How to selecting which Csound file to run on startup

	1. Log in to the Raspberry Pi
	2. Edit the script called "startup.sh" - you could for instance use the nano editor, in which you would type "nano startup.sh"


## 3. Software and firmware updates

### 3.1 Update the firware for COSMO plank:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmohat-fw" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"


### 3.2 Update the firware for COSMO HAT:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmohat-dw" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"
	5. Type "make fuse"	

### 3.3 Update the effect library from git:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmo-dsp" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"

### 3.4 Update entire image to latest version 

	CAREFUL! These operations can make your computer unusable if you mess up the commands! Read carefully!!

	You will need a SD card adapter and reader to complete these steps

	#### OS X

		1. Download the latest COSMO image file from [this location](https://drive.google.com/open?id=0B-Iu7KEexnCpOTk2N0RoY2hiaHM)
		2. Power down the COSMO and extract the SD card from underneath the Pi
		3. Insert to SD card into an adapter and the adapter into your reader
		4. Open the terminal and navigate to the folder where you have placed the COSMO image
		5. Follow these instructions carefully: [https://www.raspberrypi.org/documentation/installation/installing-images/mac.md](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)


<!-- THIS PART NEEDS REWRITING

## <a name="csound"></a>4. Basic Csound on COSMO

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
#include "/Reverb.csd"
#include "UDOs/Lowpass.csd"
```

Since the Csound code is placed in separate files, we need these lines to include the actual code for Reverb and Lowpass. If you want to use e.g. the MultiDelay effect you need to add the line **#include "UDOs/MultiDelay.csd"**

```
instr 1 
#include "../Includes/adc_channels.inc"
#include "../Includes/gpio_channels.inc"
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


-->

