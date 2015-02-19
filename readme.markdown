# IOT Enabler Kit firmware: 

**Table of Contents** 
- [Supported Boards](#supported-boards)
- [The RL78/G14 board with built-in Gainspan module](#the-rl78g14-board-with-built-in-gainspan-module)
	- [Usage Instructions](#usage-instructions)
	- [Programming Instructions](#programming-instructions)
	- [Install the Driver](#install-the-driver)
	- [Implementation Details](#implementation-details)
		- [Known Issues](#known-issues)
	- [Troubleshooting](#troubleshooting)
- [Helpful Links](#helpful-links)

A Dweet (http://dweet.io) and Freeboard (http://freeboard.io) cloud connector for Renesas 8- and 16-bit microcontrollers.  This code turns a compatible evaluation board into a real-time internet enabled device.  Once the connector is deployed to a device, the device will automatically connect to the cloud platforms and share it's peripherals using a standardized API.  This enables developers to create applications for the evaluation board in a wide variety of languages, without needing to download an SDK or physical access to the device.  

## Supported Boards

*  RL78/G14 Demonstration Kit
    *  Built-in WiFi Connectivity via Gainspan GS1011-MIPS module
    *  Support for GPS PMOD (beta)
    *  Support for cellular connectivity via Nimbelink PMOD (beta)
    *  Support for additional PMODs (in development)

## The RL78/G14 board with built-in Gainspan module

The current firmware code uses the IAR RL78 Workbench development environment.  Future code releases will support additonal IDEs including the CubeSuite+ environment and Applilet3 driver generation tool.  Notable features include:
*  Dweet credentials are automatically generated based on the device mac address, no user intervention required
*  Wifi access point can be set using the web provisioning feature of the gainspan module
*  A single firmware can be used for all RL78G14 development boards.

### Usage Instructions

1.  Connect the RDK board to a USB power source using a USB-Mini cable.

	![USB Power connection](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/RL78G13\_RDK\_PC\_connection.jpg)

1.  The RDK board now needs to be configured for an active wireless access point with an internet connection.  Hold down ```Switch 2```, Press and release the ```Reset``` button, and then release the ```Switch 2``` button.  See this video for a demonstration: [Enter Wifi Provisioning Mode](https://docs.google.com/open?id=0B_kD7ktKdpaQeTdfT3YtZERMNXM).
1.  Using a smartphone, tablet, or laptop, connect to the wireless access point indicated on the LCD screen.

	![LCD Screen Provisioning Message](http://i.imgur.com/wY5cYir.jpg)
	![Provisioning Wireless AP](http://i.imgur.com/COSvdyB.jpg)

1.  Open a web browser and go to the URL indicated on the LCD screen.  Click on the ```Wireless and Network Configuration``` link.

	![Provisioning Wireless Frontpage](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/webprovisionFrontpage.png)

1.  To scan for an access point to connect to, click on ```Select an Existing Network```

	![Provisioning Wireless Existing Network](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/webprovisionExisting.png)

1.  Pick a wireless AP from the list and click on it's ```Select``` button:

	![Provisioning Wireless Network List](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/webprovisionList.png)

1.  Enter the wireless password, leaving the other fields at default values.  Click on ```next```:

	![Provisioning Wireless Network Settings](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/webprovisionSettings.png)

1.  Click on ```Save And Apply``` to confirm the selection.

	![Provisioning Wireless Confirmation](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/webprovisionConfirmation.png)

1.  You should see the following message displayed on the LCD screen.  Press the ```RESET``` button.

	![LCD Screen Provisioning Done](http://i.imgur.com/fYaBgls.jpg)

1.  After rebooting, the device will automatically connect and begin producing data.  Note the ```ID: ``` field on the third line, and keep an eye on the screen for any errors.

	![LCD Screen when Running](http://i.imgur.com/DwSW7MW.jpg?3)

1.  You will need to re-connect to a wireless access point with an internet connection.  Navigate to [renesas.freeboard.io](http://renesas.freeboard.io/).  In the "Thing Name" field, enter the thing name displayed on the RL78 LCD and click "SET" [Note: To change the thing name after clicking SET, please refresh the page).

	![Select Board](https://raw.githubusercontent.com/buglabs/iot-enabler-kit/master/tutorial/images/rl78%20tutorial%201.png)

1.  You should now see live data from your Renesas device.  

	![Running demo](https://raw.githubusercontent.com/buglabs/iot-enabler-kit/master/tutorial/images/rl78%20tutorial%202.png)


### Programming Instructions

1.  Download and install the [Renesas Flash Programmer V2](http://am.renesas.com/products/tools/flash_prom_programming/rfp/downloads.jsp#) from [http://am.renesas.com/products/tools/flash_prom_programming/rfp/downloads.jsp#](http://am.renesas.com/products/tools/flash_prom_programming/rfp/downloads.jsp#)
1.  Locate SW5 in the middle of the RL78G14 RDK board.  Move Switch 2 of SW5 in the Off position, or towards the green square in this photo:

	![RL78G14 RDK Debug Enabled](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/RL78G14debugenabled.JPG)

1.  Connect the RDK board to the PC using a USB-Mini cable.

	![USB Power connection](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/RL78G13\_RDK\_PC\_connection.jpg)

1.  The PC should detect a new device.  If you see the following message, the driver was installed successfully and you can continue.  Otherwise, you must click the following link to [Install the Driver](#install-the-driver).

	![programming device detected by system](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashBoardDetected.png)

1.  Open ```Renesas Flash Programmer V2.00``` from the start menu.  Click on Next to create a new workspace for the RL78G14.
 
	![programming create new workspace](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashNewWorkspace.png)

1.  Select ```RL78``` from the Microcontroller dropdown.  Then select the ```R5F104PJ``` MCU from the Device Name Column.  Finally, enter ```YRDKRL78G14``` as the worksapce and project name, then click Next.
 
	![programming select the MCU](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSelectMCU.png)

1.  In the next dialog, open the Tool dropdown list, and select the lowermost COM port.  This should correspond to the COM port listed when the device was first added to the system.  Then click Next.
 
	![programming select the port](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSelectProgrammer.png)

1.  Click next through the following two dialog boxes, leaving the default values intact.
 
	![programming power supply](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashPowerSupply.png)
	![programming confirmation](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSettingsConfirmation.png)

1.  Select ```Erase``` from the Microcontroller drop down menu, then click the large Start button.  If successful, the ```PASS``` text should be visible in green.

	![programming select erase](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSelectErase.png)
	![programming erase complete](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashEraseComplete.png)

1.  Select ```Program``` from the Microcontroller drop down menu.

	![programming select program](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSelectProgram.png)

1.  Download the newest software release [from this link](https://github.com/buglabs/iot-enabler-kit/tags).  Each release is a snapshot of the entire repository.  Extract the downloaded zip file to the PC, then click on the ```Browse``` button on the Renesas Flash Progreammer, and select the .mot file that corresponds to the software release you would like to deploy:

	![programming select firmware file](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashSelectFirmware.png)

1.  Click on the large Start button.  The firmware will be deployed to the device, displaying a progress bar and percentage readout.  If successful, the ```PASS``` text should be visible in green.

	![programming in progress](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashProgrammingProgress.png)
	![programming complete](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/flashProgrammingComplete.png)

1.  Move Switch 2 of SW5 in the On position, or towards the green square in this photo:

	![RL78G14 RDK Debug Disabled](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/RL78G14debugdisabled.JPG)

1.  The new software should begin running on the device, see the user guide above.  Repeat the Erase and Program steps for each board to be programmed.

### Install the Driver

Follow these instructions to install the Virtual USB Com Port driver, required ONLY to deploy firmware to the board.  This is not required to use the board.

1.  After following the programming instructions above, and after plugging in the RL78 board to your PC, you may have seen the following error:

	![Driver Not Found](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverNotFound.png)

1.  Download the following ZIP file and extract it to a known location (like the Desktop) [Renesas USB Drivers](http://am.renesas.com/media/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrpbrl78g13/USB_Drivers.zip)	
1.  Open the Device Manager on your PC.  If you are unsure of how to do this, see [this tutorial](http://www.computerhope.com/issues/ch000833.htm)
1.  Find the RL78 board in your list of devices.  It should appear with a small yellow exclaimation point under the heading ```Other Devices``` or ```USB Devices```.  Right click on the ```Unknown Device``` and click ```Update Driver Software...```

	![Update the driver software](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverUpdateSoftware.png)
	
1.  On the next screen, direct Windows to install the driver manually by clicking on the ```Browse my computer for driver software``` button.

	![Install the driver Manually](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverInstallManually.png)
	
1.  Click on the ```Browse``` button and navigate to the folder in which you extracted the USB Drivers earlier.  In this case, they were extracted to the Desktop.  Then click ```Next```.

	![Select the driver folder](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverSelectLocation.png)
	
1.  Windows will now install the drivers.  You should be greeted by the following success screen:

	![Driver installation complete](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverInstallComplete.png)

1.  You can now delete the driver files you extracted earlier.  If you open up the Device Manager again, you will see the RL78 board correctly installed.  Note the COM Port number:

	![The correct RL78 driver entry](https://raw.github.com/buglabs/bugswarm-renesas/yrdkrl78g14/tutorial/images/DriverCorrectInstall.png)

### Implementation Details

Pseudocode for the firmware:

1.  Check status of switches.  If SW1 and SW3 are held down, enter Gainspan web demo.  If SW2 is held down, enter web provisioning mode
1.  Initialize hardware and read wireless AP data from nonvolatile storage.  If no SSID has been saved, enter web provisioning mode
1.  Read wifi MAC address and execute API call to Dweet server.  Dweet credentials will be created if the device is new, and then returned.
1.  If Dweet credentials could not be retreived from server, use default ID.
1.  Enter production loop, in which each sensor on the board is sampled and transmitted to the server, every second.

#### Known Issues

1.  The watchdog timer has not been enabled in the beta release, adding this will improve reliability when the module is suddenly disconnected from the internet.
1.  Serial debugging occurs over UART0 (at 115200 baud) which is used by the debugger.  We haven't been able to use the USB debugger tool to read this data, we instead used a seperate USB->Serial converter connected to pins 54 and 55. 
1.  Some boards come pre-loaded with an older version of firmware. Please follow the procedure detailed in [programming instructions](#programming-instructions) to update to the latest firmware.
1.  In order to enable the buzzer, please make sure the jumper on JP3 covers the top two pins, which moves the speaker output from the DAC to the PWM.
1.  If multiple development boards are online at the same time, you may experience connection issues. All RL78 boards share the same resource, which may cause failures in bi-directional communication. 
1.  Upon disconnection, your board should re-connect itself after 10 minutes. You may hit the reset button to speed this up.
1.  By default, the LED status on the RDKnext website is static. Please click on the 1 or 0 under any LED number to initiate. To turn LEDs on or off, click on the 0 or 1 under the LED number. If webpage is reset, or board ID is switched, LED status will show last configuration used until engaged.


### Troubleshooting

1.  Rebooting your device will often solve connection issues, please try this first.
1.  If an error is printed to the LCD screen on line 4 or line 8, and the error does not go away for a few minutes, try manually resetting the board.
1.  If the RDK board never appears on the web portal, use a smartphone or laptop to verify that the selected wireless access point has an internet connection, particularly to dweet.io and freeboard.io.
1.  Visit http://dweet.io/follow and input your device's Thing Name to verify successful connection to the Dweet messaging service. 
1.  Please use the most up-to-date browsers when connecting to http://renesas.freeboard.io/ (IE8 or lower will not work, and older versions of Safari, Firefox and Chrome may have difficulty displaying data). The latest version of Firefox has shown to be the most robust.
1.  Conference center hotspots often have trouble sustaining a connection. Some hotspots do not work well with the Gainspan WiFi chipset. Please try a clean hotspot with little traffic if you experience connection issues (Verizon jetpack hotspots have been tested to work).
1.  For further support on either Dweet or Freeboard, email support@buglabs.net

### Helpful Links

* [Simple RL78 Dashboard](http://renesas.freeboard.io/) - http://renesas.freeboard.io/
* [Expanded RL78 Dashboard (w/ GPS)](http://rl78.freeboard.io/) - http://rl78.freeboard.io/
* [RL78 Refrigeratior Demo](http://refrigeration.freeboard.io/) - http://refrigeration.freeboard.io/
* [Distillery Dashboard](https://freeboard.io/board/538e1353f1776c1c2e000712)
* [City Air Quality Dashboard](https://freeboard.io/board/538e1374f1776c1c2e000713)
* [Humidor Dashboard](https://freeboard.io/board/538e1392f1776c1c2e000714)
* [Dweet Homepage & Documentation](http://dweet.io/)
* [Freeboard Homepage](http://freeboard.io/)
* [YRDKRL78G14 Main Page (With Quick Start Guide)](http://www.renesas.com/products/tools/introductory_evaluation_tools/renesas_demo_kits/yrdkrl78g14/index.jsp)

