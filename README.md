# GrowLabChallenge

## Follow the steps with me

### Install the operating system

* [X] Flash micro-SD card with Raspberry Pi OS [Download the tool](https://www.raspberrypi.org/downloads)

* [X] Copy [ssh file](./config/ssh) into the boot folder of the micro-SD card

* [X] Fill [wpa_supplicant.conf.template](config/wpa_supplicant.conf.template) and rename it to wpa_supplicant.conf (without .template at the end)

* [X] Copy wpa_supplicant.conf to boot folder of the micro-SD card
* [X] Try to launch `ping raspberrypi.local` from a terminal

* [X] To ssh into your RP zero launch `ssh pi@raspberrypi.local`

* [X] Trust the RP by answering yes (only needed the first time) and enter the default password: `raspberry`

* [X] Set up un new password: `passwd`

>Optional:
As it won't harm you in any way, feel free to run a little update/upgrade...

```sh
sudo apt update
sudo apt upgrade
```

## Install Grow software

* [ ] Download it `curl -sSL https://get.pimoroni.com/grow | bash`

* [ ] The program will ask you to confirm wether or not tou want to download the examples (yes) and to reboot (yes)

## Useful stuff

* Stoping the service: `sudo systemctl stop grow-monitor.service`

* Edit configuration file:

```sh
cd /etc/default
sudo nano grow
```

## Camera

* Connect the camera cable

* Activate camera

* Test the camera with `sudo raspistill -o image.jpg`

* Transfer the file with `scp pi@raspberrypi.local:~/image.jpg Desktop/`

## Taking pictures

* git clone https://github.com/alexellis/phototimer

```sh
mkdir -p ~/image
sudo nano /lib/systemd/system/phototimer.service
```

* Copy paste the following:

```sh
[Unit]
Description=Take pictures every 2hours from 8am to 8pm
After=multi-user.target

[Service]
Type=idle
ExecStart=/usr/bin/python /home/pi/phototimer/take.py 120

[Install]
WantedBy=multi-user.target
```

* Then change the permissions on the file

```sh
sudo chmod 644 /lib/systemd/system/phototimer.service
```

* And enable the service

```sh
sudo systemctl daemon-reload

sudo systemctl enable phototimer.service
```

* Reboot and watch the service being started

> To transfer the files from the Raspberry to your local computer: `scp -r pi@192.168.1.20:~/image Desktop/`
