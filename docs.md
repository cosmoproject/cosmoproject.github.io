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


**NB!** These instructions assume you have set up your Raspberry Pi with the latest COSMO image. If you don't have this image installed, go to [section 6.4](#64-update-entire-image-to-latest-version) first.

* TOC
{:toc}

## 1. Connect

The easiest way of connecting to your Raspberry Pi/COSMO is by connecting both it and your computer to a router or some other existing network. The other solution, which is to set up a direct connection (an ethernet cable) between your computer and RPi/COSMO, involves a few more steps and can have several quirks depending on type and version of OS. 

Another option, is to connect a keyboard and screen and work directly on the Raspberry Pi

### 1.1 How to log in to the Raspberry Pi on existing network
					 
COSMO Raspbian Image login credentials

- ```login:``` **```pi```** 
- ```password:``` **```raspberry```**
- ```bonjour-name:``` **```cosmo1.local```**

For the COSMO Raspbian Image **```pi```** is the default username, **```raspberry```** is the default password and **```cosmo1.local```** is the default network name for the Pi. If you want a personal network name for your COSMO, see [How to change the network name of your COSMO](#13-how-to-change-the-network-name-of-your-cosmo))

#### OS X
1. Open Finder, go to **```/Applications/Utilities```** and open the app called **```Terminal```**
2. In the terminal you type **```ssh pi@cosmo1.local```**
3. When prompted, type in password **```raspberry```**

#### Windows
1. Download and install **```putty```** from [www.putty.org](www.putty.org/)
2. Open **```putty.exe```**
3. Type in **```cosmo1.local```** in the **```Host name or IP address```**-field. Make sure the connection type is set to **```SSH```**
4. Press **```Open```**
5. When prompted, type in username **```pi```** and password **```raspberry```**

#### Linux

1. If you're in X, open a terminal window
2. Type **```ssh pi@cosmo1.local```** 
3. When prompted, type in password **```raspberry```in**


### 1.2 How to log in to the Raspberry Pi using a direct connection 

#### OS X 
1. Connect an Ethernet cable between your computer and Raspberry Pi - make sure the lights on the RPi Ethernet port are lit (orange and green)
2. On your Mac, press the Apple logo in the top left corner and choose **```System Preferences...```**
3. Press the **```Sharing```** icon
4. Select the **```Internet Sharing```** option
5. In the dropdown menu next to **```Share your connection from```**, select **```Wi-Fi```**
6. In the list next to To computers using check the box next to **```Ethernet```** or **```Thunderbolt Ethernet```** (depening on what model your Mac is)
7. Check the box to the left of **```Internet Sharing```** (in the column named **```On```**) to start Internet Sharing
8. You will get a message box displaying a warning - push the **```Start```** button
9. Now open Finder and go to **```/Applications/Utilities```** and open the app called **```Terminal```**
10. In the terminal you type **```ssh pi@cosmo1.local```** (**```pi```** is the username we use to log on to the Pi and cosmo1.local is the network name for this Pi. If you want a personal network name for your COSMO, see [How to change the network name of your COSMO](#change-network-name))
11. This should prompt you for a password to log on to the Pi. The default password on the COSMO Raspbian Image is **```raspberry```**
12. You should now be logged on to your COSMO ready to make some crazy sounds!

**Note**: names may vary slightly depending on version of OS X

#### Windows

Coming...

#### Linux

Coming....

### 1.3 How to change the network name of your COSMO

1. Log in to the Raspberry Pi
2. Type **```raspi-config```**
3. Go to **```Advanced Options```**
4. Go to **```Hostname```**
5. Type in your desired name
6. Press ok and let the Raspberry reboot
7. You can now access your Raspberry Pi using the name you chose + *'.local'* (eg. *'myawesomecosmo.local'*)

<!-- ############################################################################################################################## -->

## 2. Solder

### 2.1 About custom COSMO hardware
These instructions are primarily for building a COSMO Box with the hardware components we provide during our workshops. Unfortunately we don't have our custom designed controller board, COSMO plank, or our custom designed stereo true bypass and dry/wet cross mixer board available for sale anywhere, but it's all open source, so if you want to produce and assemble the PCBs yourself head over to our github.

- COSMO plank schematics can be found here: [https://github.com/cosmoproject/plank](https://github.com/cosmoproject/plank)
- CrossMixer schematics can be found here: [https://github.com/cosmoproject/bypass_crossmix](https://github.com/cosmoproject/bypass_crossmix)

### 2.2 Power Supply Unit
- Solder 9V connector to the In (- ground; +) of the **MH-MINI-360** converter

<center>
<img src="/images/instructions/1_VoltageConverter.png" class="img-circle">
</center>

- Negative is center on guitar equipment!
- Connect a 9V power supply to the connector
- Use a voltmeter to test from the out(-) of the converter circuit to the input - you should see 9V
- Measure the output of the converter, which will be 9V or lower
- Use a screwdriver to adjust the screw on the circuit until you measure 5V output

<center>
<img src="/images/instructions/2b_VoltageConverterAdjust.png" class="img-circle">
</center>

- Solder the red (+) and the black (-) leads of a micro USB-cable to the output of the converter.

<center>
<img src="/images/instructions/2_VoltageConverterCable.png">
</center>

(If you're using the Cirrus Audio Logic card you can use a power jack instead of micro USB to power the Pi through the Cirrus Audio Logic card)

### 2.3 CrossMixer audio in/out

<object data="/images/instructions/CrossMixer V2 - in-send-receive-out-print.pdf#toolbar=0&navpanes=0&scrollbar=0" type="application/pdf" style="overflow:hidden" width="700px" height="985px">
    <embed src="/images/instructions/CrossMixer V2 - in-send-receive-out-print.pdf">
        This browser does not support PDFs. Please download the PDF to view it: <a href="/images/instructions/CrossMixer V2 - in-send-receive-out-print.pdf">Download PDF</a>.</p>
    </embed>
</object>

If you have V1 of the COSMO CrossMixer, download <a href="/images/instructions/CrossMixer V1 - in-send-receive-out-print.pdf">this pdf</a>

### 2.4 CrossMixer pot, LED, switch and power

<object data="/images/instructions/CrossMixer V2 - Wiring - pot_LED_switch.pdf#toolbar=0&navpanes=0&scrollbar=0" type="application/pdf" style="overflow:hidden" width="700px" height="985px">
    <embed src="/images/instructions/CrossMixer V2 - Wiring - pot_LED_switch.pdf.pdf">
        This browser does not support PDFs. Please download the PDF to view it: <a href="/images/instructions/CrossMixer V2 - Wiring - pot_LED_switch.pdf">Download PDF</a>.</p>
    </embed>
</object>

If you have V1 of the COSMO CrossMixer, download <a href="CrossMixer V1 - Wiring - pot_LED_switch.pdf">this pdf</a>


### 2.5 COSMO HAT to Raspberry Pi

The only thing needed to connect the COSMO HAT to the Pi, is to solder a 40-pin header on to the COSMO HAT and then attach the HAT on top
of the Rasperry Pi 40-pin header.

Picture coming...

### 2.6 COSMO plank to Raspberry Pi

Coming...

### 2.7 Pots, switches and LEDs

<object data="/images/instructions/COSMO plank - Wiring.pdf#toolbar=0&navpanes=0&scrollbar=0" type="application/pdf" style="overflow:hidden" width="700px" height="985px">
    <embed src="/images/instructions/COSMO plank - Wiring.pdf">
        This browser does not support PDFs. Please download the PDF to view it: <a href="/images/instructions/COSMO plank - Wiring.pdf">Download PDF</a>.</p>
    </embed>
</object>



<!-- ############################################################################################################################## -->

## 3. Assemble


### 3.1 Design your box

Lay out all your components (knobs, jacks, leds, pots) and make a design that both suits your artistic ideas and fits within the box. Remember to make enough for all the hardware on the inside! A good way of testing this, is to make a quick mockup cardboard version of your enclosure and try fitting everything in there first.

Here are some examples of COSMO-designs from previous workshops:

<img src="/images/3_COSMO_designs.JPG">

### 3.2 Drill holes into the enclosure

|Component hole sizes|
| :-----: | :---------: | :----: |   
| <img src="/images/instructions/components/stomp_switch.jpg" width="200" class="img-borderless"> | <img src="/images/instructions/components/toggle_switch.jpg" width="200" class="img-borderless">| <img src="/images/instructions/components/small_push_button.jpg" width="200" class="img-borderless">
| **Stomp Switch: 12mm** | **Toggle Switch: 6mm** | **Small Push Button: 7mm** | 
| <img src = "/images/instructions/components/stereo_pot.jpg" width="200" class="img-borderless"> | <img src = "/images/instructions/components/pot.jpg" width="200" class="img-borderless"> | <img src="/images/instructions/components/jack_635mm.jpg" width="200" class="img-borderless"> |
| **Stereo Potentiometer: 7mm** | **Mono Potentiometer: 7mm** | **6.35mm Jack (in/out): 9mm** |
| <img src="/images/instructions/components/led_5mm.jpg" width="200" class="img-borderless"> |
| **5mm LED with holder: 8mm**

### 3.3 Fit everything into the enclosure
- Mount knobs and switches
- Solder connections to the COSMO plank
- Connect USB-Soundcard or Cirrus Audio Logic HAT to RPI
- Connect Soundcard In- and Outputs to Jack connectors in the enclosure


<!-- ############################################################################################################################## -->


## 4. Configure and test


### 4.1 How to configure the COSMO plank 

1. Log in to the Raspberry Pi
2. Type **```cp cosmo-fw/cosmo.config.plank.sample .cosmo```**
3. Type **```nano .cosmo```**
4. You can now list which inputs are used for switches and which outputs are used for LEDs and change the order
5. Each analogue input will have two values, min and max, which can be used to calibrate each input (values have to be in the range from 0 to 1023) and invert the signal (setting max value as min and vica verca) 

### 4.2 How to configure the COSMO HAT 

1. Log in to the Raspberry Pi
2. Check that your boot settings are configured for COSMO HAT - see [section 6.3 Update /boot/config.txt for COSMO HAT](#63-update-bootconfigtxt-for-cosmo-hat)
3. Type **```cp cosmo-fw/cosmo.config.hat.sample .cosmo```**
4. Type **```nano .cosmo```**
5. You can now list which inputs are used for switches and which outputs are used for LEDs and change the order
6. Each analogue input will have two values, min and max, which can be used to calibrate each input (values have to be in the range from 0 to 8192) and invert the signal (setting max value as min and vica verca) 

### 4.3 How to test the COSMO plank

1. Log in to the Raspberry Pi
2. Kill any running instances of python/csound by typing **```killall python```** 3 times
3. Type **```cd cosmo-fw```**
4. Type **```python check_plank.py```**
5. All leds will blink in a binary counting pattern and you will see the values for all pots and switches when you twist and push them
6. Note down all maximum and minimum values for the analoge inputs

### 4.4 How to test the COSMO HAT

1. Log in to the Raspberry Pi
2. Kill any running instances of python/csound by typing **```killall python```** 3 times
3. Type **```cd cosmo-fw```**
4. Type **```python check_hat.py```**
5. All leds will blink in a single running light 
6. Note down all maximum and minimum values for the analoge inputs


### 4.4 How to test audio output from Csound

1. Connect speakers or headphones to the output of the COSMO 
2. Log in to the Raspberry Pi 
3. Kill any running instances of python/csound by typing **```killall python```** 3 times
4. Type **```cd cosmo-dsp```**
5. Type **```cd WorkshopTestFiles```**
6. Type **```csound audio-out-test.csd```**
7. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
8. You should now here some decending sine tones coming from the COSMO outputs
9. Press **```Ctrl-C```** (possibly twice) to stop Csound

### 4.5 How to test audio input to Csound

1. Connect an audio source to the input of the COSMO
2. Connect speakers or headphones to the output of the COSMO 
3. Log in to the Raspberry Pi 
4. Kill any running instances of python/csound by typing **```killall python```** 3 times
5. Type **```cd cosmo-dsp```**
6. Type **```cd WorkshopTestFiles```**
7. Type **```csound audio-in-test.csd```**
8. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
9. The audio coming in to the COSMO input should now be passed through Csound and out to the COSMO output. The RMS amplitude value of the input is printed in the console
10. Press **```Ctrl-C```** (possibly twice) to stop Csound

### 4.5 How to selecting which Csound file to run on startup

1. Log in to the Raspberry Pi
2. Edit the script called **```startup.sh```** - you could for instance use the nano editor, in which you would type **```nano startup.sh```**



<!-- ############################################################################################################################## -->

## 5. Program and play

Since programming COSMO can be done in many ways and have almost unlimited possibilites, we've devoted a separate page for this purpose: <a href="/dsp/">How to program COSMO</a>

Example of how to play with COSMO: 

<iframe src="https://player.vimeo.com/video/183101272" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/183101272">COSMO - Csound On Stage Music Operator</a> from <a href="https://vimeo.com/user16630343">Bernt Isak W&aelig;rstad</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

<!-- ############################################################################################################################## -->

## 6. Update

### 6.1 Update the firmware for COSMO plank

1. Log in to the Raspberry Pi
2. Type **```cd cosmo-fw```**
3. If you have changed any files within this folder, type **```git stash```**
4. Type **```git pull```**


### 6.2 Update the firmware for COSMO HAT

1. Log in to the Raspberry Pi
2. Type **```cd cosmo-fw```**
3. If you have changed any files within this folder, type **```git stash```**
4. Type **```git pull```**
5. Type **```make fuse```**	

### 6.3 Update /boot/config.txt for COSMO HAT

1. Log in to the Raspberry Pi
2. Type **```cd /boot```**
3. Type **```sudo nano config.txt```**
4. At the end of the file, there are two lines you need to delete
5. First find and delete **```dtparam=audio=on```**
6. Secondly find and delete **```dtoverlay=rpi-cirrus-wm5102```**
7. Save and reboot your Raspberry Pi

### 6.4 Update the effect library from ```git```

1. Log in to the Raspberry Pi
2. Type **```cd cosmo-dsp```** 
3. If you have changed any files within this folder, type **```git stash```**
4. Type **```git pull```**

### 6.5 Update entire image to latest version 

CAREFUL! These operations can make your computer unusable if you mess up the commands! Read carefully!!

You will need a SD card adapter and reader to complete these steps

**NB!** If you're using the COSMO HAT, you will need to make some changes to the /boot/config.txt file for it to work. See [section 6.3 Update /boot/config.txt for COSMO HAT](#63-update-bootconfigtxt-for-cosmo-hat)

#### OS X

1. Download the latest COSMO image file from [this location](https://drive.google.com/open?id=0B-Iu7KEexnCpdWVKUFRmUTdaRWc)
2. Power down the COSMO and extract the SD card from underneath the Pi
3. Insert to SD card into an adapter and the adapter into your reader
4. Open the terminal and navigate to the folder where you have placed the COSMO image
5. Follow these instructions carefully: [https://www.raspberrypi.org/documentation/installation/installing-images/mac.md](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)

#### Windows

Coming...

#### Linux 

Coming...

## 7. Other useful information

### 7.1 Edit files locally

The FTP client **Cyberduck** (can be downloaded at [https://cyberduck.io/](https://cyberduck.io/)) allows you to edit files on the Pi in your favorite text editor locally on your computer. To connect, select **```SFTP```** as connection type and enter bonjour-name, username and password (**```raspberry```**) as shown here:

<img src="/images/Cyberdyck_connection.jpg">

When you have connected, select the file you want to edit and simply hit the edit-button. This will open the file in the associated local editor and automatically upload and overwrite the file on the Pi every time you save. 

### 7.2 List Audio interfaces

```
aplay -l
aplay -L
speaker-test -c2    # Stereo Test

speaker-test -c2 -Dhw:0 # Onboard Soundcard
speaker-test -c2 -Dhw:1 # USB Soundcard/Cirrus Logic Card
```
To adjust the sound volume, use the command **```alsamixer```**

#### Cirrus Logic Audio Card (CLAC)
The input and output channels of the CLAC can be turned on and off using the scripts provided in the following folder. This also allows to use the on-board microphone of the audio card, instead of the line-in connection.

```
ls CirrusLogic/bin/
```

<!-- ############################################################################################################################## -->









