# raspi-collaborates-display
Bash Script to setup RaspberryPi as Controller for an HDMI-Connected Display in kiosk browser mode
## Setup
Guide for Raspberry Pi 4 Model B running on Raspberry Pi OS
## Headless Setup of your Raspberry Pi
In order to be able to access your Raspi without connecting keyboard or other peripherals you need to make sure that
* it's connected to your network and has internet access
* you're able to gain remote access through SSH or VNC

### Headless WIFI setup
Follow the steps of [the official guide for headless WIFI setup](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
### Headless SSH enabling
Quote from [the official Rasperry Pi guide](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)

>**3. Enable SSH on a headless Raspberry Pi (add file to SD card on another machine)**

>For headless setup, SSH can be enabled by placing a file named ssh, without any extension, onto the boot partition of the SD card from another computer. When the Pi boots, it looks for the ssh file. If it is found, SSH is enabled and the file is deleted. The content of the file does not matter; it could contain text, or nothing at all.

![screen shot of 'ssh' file in boot partition](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")