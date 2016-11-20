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
{% highlight shell %}
aplay sounds/Chord.wav
aplay -Dhw:0 sounds/Chord.wav	# Onboard Soundcard
aplay -Dhw:1 sounds/Chord.wav	# USB Soundcard
{% endhighlight %}

## Navigate in the terminal
{% highlight shell %}
ps 			# zeigt laufende Prozesse/Programme
kill xxxx	# stoppt Programme
ls			# zeigt Verzeichnisinhalt
cd Ordner  		# wechselt in Ordner
{% endhighlight %}

## Find help in terminal
{% highlight shell %}
man Befehl
Befehl --help
{% endhighlight %}

## quickly look into file content
{% highlight shell %}
cd csound
more HelloWorld.csd
{% endhighlight %}


## Nano-Editor
{% highlight shell %}
cd csound
nano HelloWorld.csd
{% endhighlight %}

## Running a Csound Patch
{% highlight shell %}
csound HelloWorld.csd
{% endhighlight %}

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
{% highlight shell %}
nano on-startup/xxx.sh
{% endhighlight %}

- Instruction how to define a fixed order for Audio-Devices in Linux [here](http://computers.tutsplus.com/articles/using-a-usb-audio-device-with-a-raspberry-pi--mac-55876)
- Webbrowser (Internet connection required)
	- lynx http://www.google.com



