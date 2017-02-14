
## 1. Setting up and connecting to the Raspberry Pi

	The easiest way of connecting to your Raspberry Pi/COSMO is by connecting both it and your computer to a router or some other existing network. The other solution, which is to set up a direct connection (an ethernet cable) between your computer and RPi/COSMO, involves a few more steps and can have several quirks depending on type and version of OS. 

## 1.1 How to log in to the Raspberry Pi on existing network

	## OS X


	## Windows

	## Linux
	

## 1.2 How to log in to the Raspberry Pi using a direct connection 

	## OS X (names may vary slightly depending on version of OS X)
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
 
	## Windows

## 1.3 How to change the network name of your COSMO

	1. Log in to the Raspberry Pi
	2. Run raspi-config
	3. Go to "Advanced ..something"
	4. Go to "Change hostname"
	5. Type in your desired name
	6. Press ok and let the Raspberry reboot
	7. You can now access your Raspberry Pi using the name you chose + '.local' (eg. 'myawesomecosmo.local')


## 2. Testing, calibrating and configuring COSMO

## 2.1 How to test the COSMO plank

	1. Log in to the Raspberry Pi
	2. Kill any running instances of python/csound by typing "killall python" 3 times
	3. Type "cd cosmohat-fw"
	4. Type "python planck.py"
	5. All leds will blink in a binary counting pattern and you will see the values for all pots and switches when you twist and push them
	6. Note down all maximum and minimum values for the analoge inputs


## 2.2 How to configure the COSMO plank or HAT
	
	1. Log in to the Raspberry Pi
	2. Type "nano .cosmo" 
	3. You can now list which inputs are used for switches and which outputs are used for LEDs and change the order
	4. Each analogue input will have two values, min and max, which can be used to calibrate each input (see bullet 6 in section 2.2) and invert the signal (setting max value as min and vica verca) 

How to calibrate the analogue inputs on COSMO plank or COSMO-HAT
	1. Log in to the Raspberry Pi
	2. Type "nano .cosmo"
	3. You can now set minimum and maximum values for all analogue inputs

## 2.3 How to test audio output from Csound

	1. Connect speakers or headphones to the output of the COSMO 
	2. Log in to the Raspberry Pi 
	3. Kill any running instances of python/csound by typing "killall python" 3 times
	4. Type "cd cosmo-dsp"
	5. Type "cd WorkshopTestFiles"
	6. Type "csound audio-out-test.csd"
	7. Make sure the COSMO Cross Mixer (if installed) is dialed to 100% wet
	8. You should now here some decending sine tones coming from the COSMO outputs
	9. Press "Ctrl-C" (possibly twice) to stop Csound

## 2.4 How to test audio input to Csound

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

## 2.5 How to selecting which Csound file to run on startup

	1. Log in to the Raspberry Pi
	2. Edit the script called "startup.sh" - you could for instance use the nano editor, in which you would type "nano startup.sh"


## 3. Software and firmware updates

## 3.1 Update the firware for COSMO plank:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmohat-fw" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"


## 3.2 Update the firware for COSMO HAT:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmohat-dw" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"
	5. Type "make fuse"	

## 3.3 Update the effect library from git:

	1. Log in to the Raspberry Pi
	2. Type "cd cosmo-dsp" 
	3. If you have changed any files within this folder, type "git stash"
	4. Type "git pull"

## 3.4 Update entire image to latest version 

	CAREFUL! These operations can make your computer unusable if you mess up the commands! Read carefully!!

	You will need a SD card adapter and reader to complete these steps

	## OS X

		1. Download the latest COSMO image file from [LINK]
		2. Power down the COSMO and extract the SD card from underneath the Pi
		3. Insert to SD card into an adapter and the adapter into your reader
		4. Open the terminal and navigate to the folder where you have placed the COSMO image
		5. Follow these instructions carefully: [LINK]



Git errors and fixes:

	1. 




Troubleshooting:

	"Can't connect to my COSMO/Raspberry Pi - WTF!?"
		- Try logging in again - sometimes it's either very slow or doesnt work immediatly after booting up
		- Try to disconnect and re-connect the ethernet cable
		- Try pinging the Pi: "ping cosmo1.local" - if this produces a reply, try ssh'ing with the ip address instead of the Bonjour name ("cosmo1.local"). If the ping command produces something like "reply from 192.168.2.5", then you can try typing "ssh pi@192.168.2.5"
		- If you are connecting to the Pi directly from your computer, try to, if possible, connect both via a router. This is normally a much more stable solution.





