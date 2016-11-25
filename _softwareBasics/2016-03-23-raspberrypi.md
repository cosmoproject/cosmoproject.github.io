---
layout: post
title: RaspberryPi
date: 2016-04-01 10:30:00
---

## Login
- Directly using a screen and keyboard on the raspberry pi: hostname -I
	- user: pi
	- pw: raspberry

- get IP adress of this RPI
```
hostname -I
```

# Connect via ssh in the terminal:
```
ssh pi@cosmopi.local
pw: raspberry
```

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



## Play a sound
```
aplay sounds/Chord.wav
aplay -Dhw:0 sounds/Chord.wav	# Onboard Soundcard
aplay -Dhw:1 sounds/Chord.wav	# USB Soundcard / Cirrus Logic Card
```

## Navigate in the terminal
```
ps 			# show running processes with PIDs
kill xxxx	# stop certain process by PID
ls			# show content of folder
cd Ordner  	# change into a folder
cd ..		# leave the folder
```

## Find help in terminal
```
man Befehl
Befehl --help
```

## quickly look into file content
```
cd csound
more HelloWorld.csd
```


## Nano-Editor
```
cd csound
nano HelloWorld.csd
```

## Running a Csound Patch
```
csound HelloWorld.csd
```



## Further materials:

# Installing Software on the RPI
```
- sudo apt-get install softwarename
```
# Software to easily view, copy and modify files on network devices
- Mac: [Cyberduck](https://cyberduck.io/?l=de)


# Startup Script
```
nano on-startup/xxx.sh
```

- Instruction how to define a fixed order for Audio-Devices in Linux [here](http://computers.tutsplus.com/articles/using-a-usb-audio-device-with-a-raspberry-pi--mac-55876)
- Webbrowser (Internet connection required)
	- lynx http://www.google.com



