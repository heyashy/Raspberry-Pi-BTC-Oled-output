# Raspberry-Pi-BTC-Oled-output

## Parts used:

- 1 x Raspberry Pi 3
- 1 x 8gb sd card for the OS
- 1 x Coupé Ninja Pi 3 Case
- 1 x Waveshare 128×32 2.23inch OLED display HAT


## Install

Create a sd card with Raspberry Pi OS Lite. Download the repo. Install Python3, and install Pillow via pip. 

## Run the script on startup

`sudo nano /lib/systemd/system/btc_stats.service`

Add this to the file:

```
[Unit]
Description=BTC Stats
After=multi-user.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/path-to-script/stats.py

[Install]
WantedBy=multi-user.target
```
Make sure you change the path to the actual path to your script and also make sure that the python 3 file is pointing to the correct location of python3

Now the unit file has been defined we can tell systemd to start it during the boot sequence :

```
sudo systemctl daemon-reload
sudo systemctl enable btc_stats.service
```
Reboot the Pi and your custom service should run:

`sudo reboot`
