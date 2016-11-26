---
layout: post
title: Csound 30 Years Maynooth - Workshop Csound and Raspberry Pi
---


## Introduction

How to log in to the Raspberry Pi:

 # Connect via ssh in the terminal:
```
ssh pi@cosmo1.local
pw: raspberry
```

	Using a direct connection (ethernet cable) between your computer and the Raspberry Pi

	OS X (names may vary slightly depending on version of OS X):
	
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
 
 Windows:
 Download and use the [Putty](http://www.putty.org/) Software for Windows to login via ssh.



## List Audio interfaces
```
aplay -l
aplay -L
speaker-test -c2	# Stereo Test

speaker-test -c2 -Dhw:0 # Onboard Soundcard
speaker-test -c2 -Dhw:1 # USB Soundcard/Cirrus Logic Card
```
- Adjust the sound volume: alsamixer

# Cirrus Logic Audio Card (CLAC)
The input and output channels of the CLAC can be turned on and off using the scripts provided in the following folder. This also allows to use the on-board microphone of the audio card, instead of the line-in connection.

```
ls CirrusLogic/bin/
```

To test audio output from Csound:

	1. Connect speakers or headphones to the output of the COSMO 
	2. Log in to the Raspberry Pi 
	3. Kill any running instances of python/csound by typing "killall python" 3 times
	4. Type "cd cosmo-dsp"
	5. Type "cd WorkshopTestFiles"
	6. Type "csound audio-out-test.csd"
	7. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
	8. You should now here some decending sine tones coming from the COSMO outputs
	9. Press "Ctrl-C" (possibly twice) to stop Csound

To test audio input to Csound:

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

# The Cosmo Effects Library
 see.. homepage

# Use a midi interface using MIDI Controller Numbers


	1. Type "cd cosmo-dsp/library"
	2. Make a local copy of "midi_cc.inc" by typing "cp midi_cc.in myMidi_cc.inc"
	3. Type "nano myMidi_cc.inc" and put in your MIDI-Controller CC-numbers
	4. "cp MidiCcExample.csd myMidiCcExample.csd"
	5. Type

