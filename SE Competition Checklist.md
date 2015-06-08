# Competition Checklist for StuyPulse Software Engineering

This guide should be followed by Software Engineering members who are working in the pit during competitions.

## Before Competition

The following should be done before the first match of competitions (before practice matches)

+ Setup power stations
	- Provide a powerstrip for electronics (battery chargers)
	- Use another powerstrip (and an extension cord if needed) for laptops
+ Setup Justin Time
	+ Open:
		+ Eclipse
		+ Git Bash
		+ Driver Station
	+ Plug in Justin Time Charger
	+ Turn off wifi adapter
		+ Right click the wifi icon on the bottom right (task bar)
		+ Open Network Settings
		+ Click Change Adapter Settings on the right side
		+ Right click the Wifi adapter and click "Disable"
	+ Create a new Git branch (preferably the name of the competition: i.e. NYC-Regional-2015)
	
	 	`git checkout -b NYC-Regional-2015`
+ Setup the OI
	+ Make sure the following items are in the Pelican case:
		+ USB - Ethernet Adapter
		+ USB Hub
		+ 2 Gamepads
		+ OI
		+ OI Charger
	+ Start charging the OI (We don't want it to die right before the match, then it has to be set up again)
	+ Log into the Driver account
	+ Go into the utilities tab and open the Java Smart Dashboard if it has not opened already
+ Run a systems check (All moving parts of the robot bound to controls need to be tested)
	+ Connect with a printer cable or with ethernet cable + USB to Ethernet adapter
		+ If using the USB to Ethernet adapter, the USB end must be connected to the roboRIO and the ethernet end should be connected to Justin Time
	+ If anything is wrong with the robot or with the code, repair or fix it.
+ Configure the router for competition
	+ Bring to front desk and configure with FRC utilities to work with the FMS
	+ Make sure the router is set to bridge mode
	+ Connect to the robot
+ Run a second systems check to ensure that the configured radio works correctly

## During Competition

The following should be done during the time of competition.

### Before the Team Needs to Queue

+ Run a systems check
+ Make sure the OI is charged past 65%
+ Make sure the OI has all the necessary items inside the Pelican case
	+ USB - Ethernet Adapter
	+ USB Hub
	+ 2 Gamepads
	+ OI
	+ OI Charger
+ Make sure the OI is with the Drive Team, robot, or robot cart

### When the Team Is Playing In A Match

You can go watch the match if there is nothing else to do. Make sure to take note if anything goes wrong if you do.

+ Make sure there is a clean and organized workstation
+ Make sure there is one spot for the OI (empty and cleared out enough so the Pelican case can be picked up and dropped on the spot without breaking anything)
+ Worked on anything that you are supposed to work on

### Before the Drive Team Returns From the Match

+ Clear out OI spot
+ Prepare for a systems check

### After Drive Team Returns

+ Run a systems check

## Throughout Competition

+ If you lend any materials, record who lent it, who borrowed it, which team, etc. WRITE IT DOWN!
+ If any teams need help, go over and help them. It benefits the Gracious Professionalism Award

## After Competition

+ Re-enable wifi adapter (see 'Before Competition > Setup Justin Time' section for steps)
+ Push all commits to the branch you created at the beginning of the competition.
+ Pack all SE Equipment
	+ Gray Bag
		+ Justin Time
		+ No Knowey
		+ No Wangey
		+ Justin Time Charger
		+ No Knowey/No Wangey Charger
		+ Printer Cables (optional)
	+ Black Bag
		+ Acer Laptop
		+ Gamepads (should have 2-3 depending on how many were packed)
		+ Acer Laptop charger
		+ All other cables related to laptops or computers
	+ Anything else that was packed
+ Zip-tie the SE Crate

## Issues and Fixes

+ **Cannot get comms**
	+ Make sure there is no proxy set on the laptop
	+ Make sure DNS and IPv4 Address are set to 'Automatic'
		+ Right click the wifi icon on the bottom right (task bar)
		+ Open Network Settings
		+ Click Change Adapter Settings on the right side
		+ Right click the Wifi adapter and click "Properties"
		+ Scroll down to the bottom
		+ Click / Highlight 'IPv4 ... '
		+ Click Properties
		+ Check "Automatically assign/detect" for both the IP Address and the DNS
	+ Make sure the radio is on bridge mode
	+ There is a bug with the radio not saving settings correctly through the configuration tool
		+ While the radio is on, acquire a thin tip (such as a paper clip) and manually click the reset button on the back of the radio
		+ Connect to the radio manually (10.6.94.1) and un-check and then re-check all the options manually, then save
	+ Check if the roboRIO is connected
		+ roborio-694.local
	+ Re-configure the radio at the front desk
	+ Replace ethernet cables (use straigh-through cables)
	+ Make sure the Driver Station is configured to use the correct year's FMS
	+ Restart Driver Station
+ **Driver Station not functioning, not detecting gamepads**
	+ Restart the computer and re-open all the programs that are supposed to be open
+ **Flashing the roboRIO**
	+ Open a file browser and go to the following path:

		```
	C:\Program Files (x86)\National Instruments\LabVIEW 2014\project\roboRIO Tool
		```
	+ If that path does not exist, use:

		```
	C:\Program Files\National Instruments\LabVIEW 2014\project\roboRIO Tool
		```
	+ Run ```roboRIO_ImagingTool```
	+ The tool will automatically search for roboRIO targets that are connected to the computer
	+ Enter your team number in the text box in the top right
	+ Make sure the "Format Target" checkbox is checked
	+ Select the image. There should be images already located in the lower left box. Select the correct version, and click "Reformat"
	+ roboRIO images will be in:

		```
	C:\Program Files (x86)\National Instruments\LabVIEW 2014\project\roboRIO Tool\FRC Images
		```
+ **Updating the PCM, PDP, and other things**
	+ Connect to the roboRIO
	+ Open an internet browser
	+ Go to ```roborio-694.local```. If this is being done for another team, then change 694 to the team number. (i.e. For Team 9876, go to ```roborio-9876.local```)
		+ If this window does not open, make sure Microsoft Silverlight is the latest version.
	+ Click "Login" in the top right
	+ Enter "admin" as the username and hit enter.
	+ Select the system you want to reflash, and click "Update Firmware" in the bottom right
	+ A window will pop up, navigate to:

		```
	C:\Users\Public\Documents\FRC
		```
	+ Select the .crf file for the system (PCM-Application-1.62.crf for a 2015 PCM, PDP-Application-1.40.crf for a 2015 PDP, etc.)
	+ Click "Open"
	+ Click "Begin Update"

+ **Clearning a Sticky Fault (system is blinking orange)**
	+ Connect to the roboRIO
	+ Open an internet browser
	+ Go to ```roborio-694.local```. If this is being done for another team, then change 694 to the team number. (i.e. For Team 9876, go to ```roborio-9876.local```)
		+ If this window does not open, make sure Microsoft Silverlight is the latest version.
	+ Select system with a Sticky Fault
	+ Rapidly click "Self Test" until the screen displays "Faults cleared!"
