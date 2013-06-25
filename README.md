arduino-xpl-heatpump-controller
=====================================

Control a Panasonic heat pump/split unit air conditioner with Arduino using the xPL protocol
Currently supports at least models 
* Panasonic E9/E12-CKP and E9/E12-DKE (Panasonic remote control P/N A75C2295 and P/N A75C2616)
* Midea MSR1-12HRN1-QC2 + MOA1-12HN1-QC2, sold as Ultimate Pro Plus Basic 13FP in Finland (Midea remote control P/N RG51M1/E)

Some xPL-perl example commands:

    xpl-sender -m xpl-cmnd -t xpl-arduino.heatpumpctrl -c aircon.ckp power=0 mode=2 fan=3 temperature=23
    xpl-sender -m xpl-cmnd -t xpl-arduino.heatpumpctrl -c aircon.dke power=0 mode=2 fan=3 temperature=23
	xpl-sender -m xpl-cmnd -t xpl-arduino.heatpumpctrl -c aircon.midea power=0 mode=2 fan=3 temperature=23
	
Supported parameters
* Common to Midea and Panasonic CPK and DKE-series
    * power
	    * OFF: 0
		* ON: 1
		* Note! There is no direct ON/OFF command on the Panasonic CKP series. As a workaround the timer is set to stop or start the unit in one minute from the current time
	* mode
        * AUTO: 1
	    * HEAT: 2
	    * COOL: 3
	    * DRY: 4
	    * FAN: 5
		* FP: 6 (Midea only)
    * fan (Midea only up to 4)
	    * AUTO: 1
		* FAN1: 2
		* ...
		* FAN5: 6
    * temperature
	    * 16 .. 30 (Panasonic)
		* 17 .. 30 (Midea)
    * vswing (Panasonic only)
	    * AUTO: 1
		* UP: 2
		* ...
		* DOWN: 6
* Panasonic CPK only
	* hswing
	    * AUTO: 1
		* MANUAL: 2
* Panasonic DKE only
    * hswing
	    * AUTO: 1
		* middle: 2
		* left: 3
		* middle left: 4
		* right: 5
		* middle right: 6
		
Schema
------

Bill of materials
* Arduino :)
* Arduino Ethernet shield
* IR led
* 1 kOhm resistor for the IR led
		
Connect an IR led (with 1k resistor in series) between GND and digital pin 3

![Schema](https://raw.github.com/ToniA/arduino-xpl-heatpump-controller/master/arduino_irsender_bb.png)
