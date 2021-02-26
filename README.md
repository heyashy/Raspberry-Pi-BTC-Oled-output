# Raspberry-Pi-BTC-Oled-output

Inline-style: 
![alt text](https://cdn.hackaday.io/images/5448561614347574915.jpg)


## Parts used:

- 1 x Raspberry Pi 3
- 1 x 8gb sd card for the OS
- 1 x Coupé Ninja Pi 3 Case
- 1 x Waveshare 128×32 2.23inch OLED display HAT

## Libraries Installation

Open terminal of Raspbain and install libraries (BCM2835, wiringPi, Python) as below

```
#Installing BCM2835 library, for more details of the libraries, you can refer ti its website: http://www.airspayce.com/mikem/bcm2835/
wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.60.tar.gz
tar zxvf bcm2835-1.60.tar.gz
cd bcm2835-1.60/
sudo ./configure
make
sudo make check
sudo make install

#Installing wiringPi libraries, sudo apt-get install wiringpi
#For Pi 4, you need to update it
cd /tmp
wget https://project-downloads.drogon.net/wiringpi-latest.deb
sudo dpkg -i wiringpi-latest.deb
gpio -v

#Installing python libraries
#python2
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install python-pil
sudo apt-get install python-numpy
sudo pip install RPi.GPIO
sudo pip install spidev
#python3
sudo apt-get update
sudo apt-get install python3-pip
sudo apt-get install python3-pil
sudo apt-get install python3-numpy
sudo pip3 install RPi.GPIO
sudo pip3 install spidev
```

## Install

Create a sd card with Raspberry Pi OS Lite. Download the repo. Install Python3, and install Pillow via pip. 

## Run the script as a service on boot

To run the script on startup, run the following command

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
