
Debugging:

How to log in to the Raspberry Pi:

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

How to change the network name of your COSMO:
	1. Log in to the Raspberry Pi
	2. Run raspi-config
	3. Go to...



To test the COSMO plank:

	1. Log in to the Raspberry Pi
	2. Kill any running instances of python/csound by typing "killall python" 3 times
	3. Type "cd cosmohat-fw"
	4. Type "python planck.py"
	5. All leds will blink in a binary counting pattern and you will see the values for all pots and switches when you twist and push them

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

Update the effect library from git
	1. Log in to the Raspberry Pi
	2. Type "cd cosmo-dsp" 
	3. Type "git pull"
	4. If you get errors, see 

Git errors and fixes:
	1. 

Selecting which Csound file to run on bootup:
	1. Log in to the Raspberry Pi
	2. Edit the script called "startup.sh" - you could for instance use the nano editor, in which you would type "nano startup.sh"


Troubleshooting:

	"Can't connect to my COSMO/Raspberry Pi - WTF!?"
		- Try logging in again - sometimes it's either very slow or doesnt work immediatly after booting up
		- Try to disconnect and re-connect the ethernet cable
		- Try pinging the Pi: "ping cosmo1.local" - if this produces a reply, try ssh'ing with the ip address instead of the Bonjour name ("cosmo1.local"). If the ping command produces something like "reply from 192.168.2.5", then you can try typing "ssh pi@192.168.2.5"
		- If you are connecting to the Pi directly from your computer, try to, if possible, connect both via a router. This is normally a much more stable solution.





