
# Public Lab Pi Camera Kit (Pi-Cam 01)

This project is designed to easily generate bootable SD card images from a plain "Raspbian" original image, with additional software already installed and configured. The output images are made available for download and flashing onto an SD card (see below). 

You can do this from the GitHub repository directly by opening a pull request, which will trigger a new image to be built. 

The Public Lab Pi Camera Kit includes an operating system which is built upon the efforts of many people.

The build scripts have been forked from the Hypriot project.

## Tested on

* Raspberry Pi Zero W
* Raspberry Pi 3 Model B
* add more in this issue: https://github.com/publiclab/pi-builder/issues/63

## Build instructions

**Easy pull request build process**

The easiest way to generate a new image is to open a pull request with changes to the basic image; a new one will be generated by GitLab and be available for download and flashing onto an SD card. See [pull requests](https://github.com/publiclab/image-builder-pi/pulls) for examples of this, with downloadable images already built. 

**Automatic build**: For the purposes of facilitating quick development of this image, we've setup [automatic builds](https://jenkins.laboratoriopublico.org/job/Raspberry%20Kit%20Image/) on git commits to **master** branch. 

Download the [latest development build here](https://jenkins.laboratoriopublico.org/job/Raspberry%20Kit%20Image/ws/hypriotos-rpi-dirty.img.zip).

Pre-requisites for running locally: You'll need to have Docker installed.

```
make sd-card
```

This will create an image called `hypriotos-rpi-dirty.img.zip`.

## Flash instructions

You can use the cross-platform Etcher program to flash the output images onto an SD card: https://etcher.io

You can also use the [Hypriot flash tool](https://github.com/hypriot/flash)

```
git clone https://github.com/hypriot/flash
cd flash
./flash ~/location_of/hypriotos-rpi-dirty.img.zip
```

## Usage instructions

Place the flashed microSD card into your Pi device, power it up and give it a minute or two to start the embedded access point `00-PiCamera`, with password `publiclab`.

Once you are connected to this wifi network, the Pi has hostname `pi` with IP address `172.24.1.1` and can be reached with from the `pi.local` or `pi.localdomain` address (either avahi or dns).

By default a user called **publiclab** is created with same password.

Features:
  - ssh service on port 22
  - Lighthttp on port 80
  - Flash tool can customize image at **flash time**

Desired in the short term:
  - Camera is pre-enabled
  - USB OTG is also enabled (with IP address `192.168.7.2`)

Check planning issue [5](https://github.com/publiclab/image-builder-rpi/issues/5) for other plans.

We've disabled for build performance:
  - Docker tools
