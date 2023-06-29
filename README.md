# RBPi Headless Configuration

Setting up a GUI version of a Raspberry Pi can be easy and straightforward due to the wizard on startup.

However, if using a cheaper and less powerful board such as the Zero W for your project, you may have to set it up to run headless (no GUI).

Below are a few steps you can follow to pre-configure the WiFi connection, username & password and SSH.

## WiFi

In the root of your Raspberry Pi SD card with Raspbian installed, create a wpa_supplicant.conf file with the following contents:

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=<Country Code>
network={
     ssid="<SSID>"
     psk="<PASSWORD>"
     scan_ssid=1
}
```

Replace your country code (e.g. `UK` for the United Kingdom or `US` for the United States), WiFi SSID and password. With the wpa_supplicant.conf file setup, your Raspberry Pi will try connecting to the configure WiFi on startup.

## Enable SSH

In the root of your Raspberry Pi SD card with Raspbian installed, create an empty ssh file.

When starting up, your Raspberry Pi will enable SSH if the ssh file is present.

## Configure username & password

Gone are the days when the default username was `pi` and the default password was `raspberry`.

With the latest version of Raspbian, you will have to setup your own username and encyrpted password.

In the root of your Raspberry Pi SD card with Raspbian installed, create a userconf file with the following contents:

```
username:encrypted-password
```

To get an encrypted password, use `echo 'mypassword' | openssl passwd -stdin` and paste the result in place of encrypted-password in the file.

With all that set up, you should be able to `ssh username@raspberrypi-ip-address`.

## Enabling SPI interface

Once you can successfully SSH into your Raspberry Pi, run `sudo raspi-config`.

Within the menu that opens up, visit `Interface Options` and select SPI to enable/disable the SPI kernel module.

After changing the setting, it may be worth restarting your Raspberry Pi with `sudo reboot -h now`.
