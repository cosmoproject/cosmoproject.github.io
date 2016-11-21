---
layout: post
title: RaspberryPi
date: 2016-04-01 10:30:00
---

## Login
- Mit Tastatur und Bildschirm: hostname -I
	- user: pi
	- pw: raspberry

- IP Adresse des Raspi
{% highlight shell %}
hostname -I
{% endhighlight %}

# Connect via ssh in the terminal:
{% highlight shell %}
ssh pi@raspberrypi.local
pw: raspberry
{% endhighlight %}

Download and use the [Putty](http://www.putty.org/) Software for Windows to login via ssh.


## List Audio interfaces
{% highlight shell %}
aplay -l
aplay -L
speaker-test -c2	# Stereo Test

speaker-test -c2 -Dhw:0 # Onboard Soundcard
speaker-test -c2 -Dhw:1 # USB Soundcard
{% endhighlight %}
- Adjust the sound volume: alsamixer


## Play a sound
```
aplay sounds/Chord.wav
aplay -Dhw:0 sounds/Chord.wav	# Onboard Soundcard
aplay -Dhw:1 sounds/Chord.wav	# USB Soundcard
```

## Navigate in the terminal
```
ps 			# zeigt laufende Prozesse/Programme
kill xxxx	# stoppt Programme
ls			# zeigt Verzeichnisinhalt
cd Ordner  		# wechselt in Ordner
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

## using the GPIO Pins
Buch S. 443-448

<img src="{{ site.baseurl }}/pics/GPIO_Pin1.png" width="450">
<img src="{{ site.baseurl }}/pics/GPIO_AllPins.png" width="450">


## Furhter:

# Installing Software on the RPI
- sudo apt-get install softwarename

# Software to easily view, copy and modify files on network devices
- Mac: [Cyberduck](https://cyberduck.io/?l=de)


# Startup Script
```
nano on-startup/xxx.sh
```

- Instruction how to define a fixed order for Audio-Devices in Linux [here](http://computers.tutsplus.com/articles/using-a-usb-audio-device-with-a-raspberry-pi--mac-55876)
- Webbrowser (Internet connection required)
	- lynx http://www.google.com



