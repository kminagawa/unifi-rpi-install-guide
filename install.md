# Installing Unifi Network Application on Raspberry Pi
Installation steps for installing Ubiquiti's Unifi Network Application are not quite well-documented, and so I've put together a concise guide based on recent experience.  Note that this guide was created using the Raspberry Pi 2B.

## Raspberry Pi Image
These steps are not extensive and you should follow standard guides for the setup of your version of the Raspberry Pi.
* Download the latest image for your version of Raspberry Pi: https://downloads.raspberrypi.org/raspios_full_armhf/images/raspios_full_armhf-2022-09-26/2022-09-22-raspios-bullseye-armhf-full.img.xz.torrent
* Flash the image to an SD Card using Balena Etcher: https://www.balena.io/etcher/
* Start up the Pi and set it up as usual (Not covered by this guide)
* Enable SSH after startup (Not covered by this guide)

## Unifi Installation
* SSH to your Pi: `ssh user@your_pi_ip`
* Add Repo Key: `sudo wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -`
* Add Raspbian Repo: `sudo echo 'deb http://archive.raspbian.org/raspbian stretch main contrib non-free rpi' | sudo tee /etc/apt/sources.list.d/raspbian_stretch_for_mongodb.list`
* Install packages:
```
sudo apt update
sudo apt install openjdk-8-jre-headless jsvc libcommons-daemon-java -y
sudo apt install mongodb-server mongodb-clients -y
```
* Download the Unifi application: `sudo curl -k https://fw-download.ubnt.com/data/unifi-controller/a195-debian-7.2.95-8f44275f0c264d24afca8712c5b8dd85.deb -o a195-debian-7.2.95-8f44275f0c264d24afca8712c5b8dd85.deb`
* Unpack the Unifi application: `sudo dpkg -i a195-debian-7.2.95-8f44275f0c264d24afca8712c5b8dd85.deb`
* Check the status of the Unifi service: `sudo systemctl status unifi`

## Accessing Unifi
The typical local address for accessing the Unifi UI is usually https://localhost:8443, but replace localhost here with your Pi's IP and you should be good to go.
