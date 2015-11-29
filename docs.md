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
![cosmobox]({{ site.baseurl }}/images/instructions/1_VoltageConverter.jng)
- Negative is center on guitar equipment
- connect 9V power supply to the connector
![cosmobox]({{ site.baseurl }}/images/instructions/2_VoltageConverterCable.jng)
- Use a voltmeter to test from the out(-) of the converter circuit to the input, you should see the 9V
- measure the output of the converter, which will be 9V or lower
- use a screwdriver to adjust the screw on the circuit until you measure 5V output
- solder the red (+) and the black (-) leads of a micro USB-cable to the output of the converter.


##2. Setting up the Raspberry Pi
- copy our (insert LINK here!) Raspian Image to a 4GB micro SD card
- connect the micro USB from the power converter cable to the Raspberry Pi 2 (RPI), it should boot up
- connect the RPI to your computer via Ethernet connection
- open the terminal/console on your mac or linux computer
- find the RPI network adress: "arp -an" 
- login: "ssh pi@169.254.38.74 (ssh pi@raspberrypi.local)"
- pw: raspberry
- test csound: "cd cosmo-dsp/WorkshopTestFiles/"
- run: "csound audio-out-test.csd"
- press Cmd+C to stop Csound
- run: "logout"
- turn off the RPI by unplugging the mini usb power

##3. Prepare the COSMO-HAT 
- solder the 40 Pin connector to the COSMO Hat
- solder the rainbow cable to the analog input channels (brown = 0)
- solder the rainbow cable to the digital input/output channels (brown = 0)
- solder middle of potentiometers to analog ins, or tip of jack connectors



##4. Setup RPI with COSMO-HAT
- attach the COSMO Hat to the RPI (no power!)
- log into RPI using SSH (Step 2)
- run: ~/cosmohat-fw $ make fuse

