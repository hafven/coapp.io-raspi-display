# coapp.io-raspi-display
Bash Script to setup RaspberryPi as Controller for an HDMI-Connected Display in kiosk browser mode
## Setup using SSH
Guide for Raspberry Pi 4 Model B running on Raspberry Pi OS with the default configuration including Raspberry Pi Desktop and given that you already can establish an SSH-connection.

Read more on how to set up your Raspi if you do not use a monitor or keyboard to run your Pi (known as headless) in the section *Headless Setup of your Raspberry Pi* below.

If you need to reset to *factory defaults* use the [Raspberry Pi Imager](https://www.raspberrypi.org/software/).

1. Determine your Raspi's local IP address
1. Establish SSH connection to your Raspi
`ssh pi@XXX.XXX.XXX.XXX`
1. if you haven't changed the default user credentials yet login using the default user name `pi` and default password `raspberry`
1. once your ssh connection is established change the default password by using the configuration wizard `sudo raspi-config` > `System Options` > `Password`
1. download the setup script to your raspi and save it in your home directory in the file `~/setup-raspi-kiosk.sh`
    ```
    curl https://raw.githubusercontent.com/hafven/coapp.io-raspi-display/main/setup-raspi-kiosk.sh > ~/setup-raspi-kiosk.sh
    ```
1. run the bash script you just downloaded as root and provide the input when asked
    ```
    sudo bash ~/setup-raspi-kiosk.sh
    ```
1. if no errors occured your raspi is now ready to serve as [coapp.io](https://www.coapp.io/) community display and show live information from your community in your spaces. After reboot it will display this in full screen (kiosk mode). By default your display will be automatically switched off (standby) at 8pm local time daily and switched on (if they are still in standby) at 8am daily, and whenever the raspi is rebooted. Confirm that it's working by rebooting the raspi through running the following command.
    ```
    sudo reboot
    ```

## created files
The setup script has created/edited the following files on your raspi:
* ~/hdmipoweron.sh
* ~/hdmipoweroff.sh
* /etc/xdg/lxsession/LXDE-pi/autostart

You can customize them by using `vi` like so.
```
vi /etc/xdg/lxsession/LXDE-pi/autostart
```
## created cronjobs
The setup has created entries to schedule daily execution of the power on/off scripts using crontab. If you want to edit this configuration do so by running the following command
```
crontab -e
```
---
# How to: Headless Setup of your Raspberry Pi
In order to be able to access your Raspi without connecting keyboard or other peripherals you need to make sure that
* it's connected to your network and has internet access
* you're able to gain remote access through SSH or VNC

#### Headless WIFI setup
Follow the steps of [the official guide for headless WIFI setup](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)

Example of the contents of the wifi configuration file ```wpa_supplicant.conf``` at Hafven
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1
country=DE
network={
 ssid="Hafven"
 psk="***********"
}
```

#### Headless SSH enabling
Quote from [the official Rasperry Pi guide](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)

>**3. Enable SSH on a headless Raspberry Pi (add file to SD card on another machine)**

>For headless setup, SSH can be enabled by placing a file named ssh, without any extension, onto the boot partition of the SD card from another computer. When the Pi boots, it looks for the ssh file. If it is found, SSH is enabled and the file is deleted. The content of the file does not matter; it could contain text, or nothing at all.

![screen shot of 'ssh' and 'wpa_supplicant.conf' file in Raspberry Pi OS boot partition](https://github.com/hafven/raspi-collaborates-display/blob/main/images/screenshot-ssh-file.png?raw=true "Logo Title Text 1")