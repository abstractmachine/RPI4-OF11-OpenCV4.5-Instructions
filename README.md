# RPI 4 Installation

These are the steps I've been using recently to build a command-line only Raspberry PI 4 image with openFrameworks 11 and OpenCv 4.5.x. This has been tested with the Raspberry Pi 4b and Compute Module 4.

Note: that we will be using raw OpenCV calls, and not depending on the openFrameworks libraries that are out of date and not well maintained. Plus, we want to use "as-is" the latest OpenCv C++ examples found online and in computer vision forums, courses, books, and training guides.

Note: I have yet to figure out how to install openFrameworks on Raspberry OS 64. According to Q-Engineering, you can get significant speed increases with 64-bit Raspberry OS, so I will have to figure this out at some time. Cf. [https://qengineering.eu/install-opencv-4.5-on-raspberry-64-os.html]()

## Raspberry Pi 4
Using OpenCv requires a decent amount of RAM, but I have not been able to fully take advantage of all 8GB of the RPI4, despite numerous attemps. Most of my uses — for example processing full 1280 x 720 HDMI video feeds — seem to work fine with a 4GB Raspberry. I have not tested with 2GB Raspberry 4.

- [Raspberry Pi 4 Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
- [Kubii](https://www.kubii.fr) (France)
- [Raspberry Pi 400](https://www.kubii.fr/raspberry-pi-400/3084-kits-raspberry-pi-400-3272496302914.html)
- [Raspberry Pi 4 Modèle B](https://www.kubii.fr/174-raspberry-pi-4-modele-b)
- [Compute Module 4](https://www.raspberrypi.org/products/compute-module-4/?variant=raspberry-pi-cm4001000)
  - [Compute Module IO Board](https://www.raspberrypi.org/products/compute-module-4/?variant=raspberry-pi-cm4001000)
  - [How to Make a Raspberry Pi Compute Module 4 Carrier Board in KiCad](https://www.youtube.com/watch?v=ypcPJC_umPQ)

## Capture Device
I have been using the Raspberry Cameras (infrared and standard models) that use the integrated camera interface, as well at the El Gato Camlink 4k capture cards for HDMI capture. I have tried many HDMI capture solutions that convert HDMI signals into the standard interface, including the Auvidea B101 and Chinese knockoffs. So far, no sucess at a stable installation with HDMI > CSI.

- [Camera Module v2](https://www.raspberrypi.org/products/camera-module-v2/)
- [Camera Module v2 Infrared](https://www.kubii.fr/idees-cadeaux/1654-nouvelle-camera-infrarouge-v2-8mp-kubii-640522710898.html) (France)
- [130° Infrared Camera with illumination](https://www.kubii.fr/cameras-accessoires/2333-raspberry-pi-camera-fisheye-grand-angle-5mp-kubii-3272496012561.html)
- [Elgato Camlink 4k](https://www.elgato.com/fr/cam-link-4k)
- HDMI to CSI
  - [HDMI to CSI](https://www.kubii.fr/convertisseurs-adaptateurs-raspberry/3210-adaptateur-hdmi-vers-csi-camera-raspberry-pi-3272496305359.html) (France)
  - [Auvidea B101](https://auvidea.eu/b101-hdmi-to-csi-2-bridge-15-pin-fpc/)
    - Raspberry Forum discussing Auvidea setup: [https://www.raspberrypi.org/forums/viewtopic.php?t=216903#p1437501]()
    - [Raspberry Pi 4: OpenCV with Auvidea B101 HDMI to CSI-2 Bridge on Raspbian 10](https://www.youtube.com/watch?v=2In8TEsvMQM) (this got me close, but remains unstable)

## Screen
Touch screens are handy for installations, or for the final project. There are official, and stuff from China that works but with wonky resolution stretching and that cannot always be (easily) configured.

- [Official 7" Screen](https://www.kubii.fr/ecrans-afficheurs/1131-ecran-tactile-officiel-7-800x480-kubii-640522710829.html)
- [3.5" Screen](https://www.amazon.fr/dp/B08HVDLHRW/)
- [7" Screen](https://www.amazon.fr/dp/B085NHF15M)

## SD Card
Start with a blank SD card.

- Tests
  - [Raspberry PI Micro SD Cards](https://www.tomshardware.com/best-picks/raspberry-pi-microsd-cards)
- Current cards I've been using:
  - [SanDisk MAX ENDURANCE microSDHC](https://www.amazon.fr/dp/B084CJ96GT)
  - [SanDisk Ultra MicroSDHC](https://www.amazon.fr/gp/product/B073K14CVB)

## Download Raspberry PI OS Lite
- [https://www.raspberrypi.org/software/operating-systems/]()

## Install onto SD Card
- [https://www.raspberrypi.org/software/]()

## Configure PI
- 

