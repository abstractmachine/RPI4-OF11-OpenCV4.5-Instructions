# RPI 4 Installation

These are the steps I've been using recently to build a command-line only Raspberry PI 4 image with openFrameworks 11 and OpenCv 4.5.x. This has been tested with the Raspberry Pi 4b and Compute Module 4.

Note: that we will be using raw OpenCV calls, and not depending on the openFrameworks libraries that are out of date and not well maintained. Plus, we want to use "as-is" the latest OpenCv C++ examples found online and in computer vision forums, courses, books, and training guides.

Note: I have yet to figure out how to install openFrameworks on Raspberry OS 64. According to Q-Engineering, you can get significant speed increases with 64-bit Raspberry OS, so I will have to figure this out at some time. Cf. [https://qengineering.eu/install-opencv-4.5-on-raspberry-64-os.html]()

## Raspberry Pi 4
Using OpenCv requires a decent amount of RAM, but I have not been able to fully take advantage of all 8GB of the RPI4, despite numerous attemps. Most of my uses — for example processing full 1280 x 720 HDMI video feeds — seem to work fine with a 4GB Raspberry. I have not tested with 2GB Raspberry 4.

- [Raspberry Pi 4 Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
- [Kubii](https://www.kubii.fr) (France for me), see Raspberry website for local distributors of each product
- [Raspberry Pi 400](https://www.kubii.fr/raspberry-pi-400/3084-kits-raspberry-pi-400-3272496302914.html)
- [Raspberry Pi 4 Modèle B](https://www.kubii.fr/174-raspberry-pi-4-modele-b)
- [Compute Module 4](https://www.raspberrypi.org/products/compute-module-4/?variant=raspberry-pi-cm4001000)
  - [Compute Module IO Board](https://www.raspberrypi.org/products/compute-module-4/?variant=raspberry-pi-cm4001000)
  - [How to Make a Raspberry Pi Compute Module 4 Carrier Board in KiCad](https://www.youtube.com/watch?v=ypcPJC_umPQ)

## Capture Device
I have been using the Raspberry Cameras (infrared and standard models) that use the integrated camera interface, as well as the El Gato Camlink 4k capture cards for HDMI capture. I have tried many HDMI capture solutions that convert HDMI signals into the standard interface, including the Auvidea B101 and Chinese knockoffs. So far, no sucess at a stable installation with HDMI > CSI.

- [Camera Module v2](https://www.raspberrypi.org/products/camera-module-v2/)
- [Camera Module v2 Infrared](https://www.kubii.fr/idees-cadeaux/1654-nouvelle-camera-infrarouge-v2-8mp-kubii-640522710898.html) (Kubii)
- [130° Infrared Camera with illumination](https://www.kubii.fr/cameras-accessoires/2333-raspberry-pi-camera-fisheye-grand-angle-5mp-kubii-3272496012561.html)
- [Elgato Camlink 4k](https://www.elgato.com/fr/cam-link-4k)
- HDMI to CSI
  - [HDMI to CSI](https://www.kubii.fr/convertisseurs-adaptateurs-raspberry/3210-adaptateur-hdmi-vers-csi-camera-raspberry-pi-3272496305359.html) (Kubii)
  - [Auvidea B101](https://auvidea.eu/b101-hdmi-to-csi-2-bridge-15-pin-fpc/)
    - Raspberry Forum discussing Auvidea setup: [https://www.raspberrypi.org/forums/viewtopic.php?t=216903#p1437501]()
    - [Raspberry Pi 4: OpenCV with Auvidea B101 HDMI to CSI-2 Bridge on Raspbian 10](https://www.youtube.com/watch?v=2In8TEsvMQM) (this got me close, but remains unstable)

## Screen
Touch screens are handy for installations, or for the final project. There are official screens, and stuff from China that works but with wonky resolution stretching and that cannot always be (easily) configured.

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
Download either the Raspberry Pi with Desktop, or the Lite. You can directly download and install these images from the official Pi Imager software in the next step.

- [https://www.raspberrypi.org/software/operating-systems/]()
- This how-to uses the following image from 2021-03-04:
  - [https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2021-03-25/2021-03-04-raspios-buster-armhf-lite.zip]()
  - [https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2021-03-25/2021-03-04-raspios-buster-armhf-lite.zip.torrent]() (Torrent)

## Install onto SD Card
- [Raspberry Pi Imager](https://www.raspberrypi.org/software/)
- [Balena Etcher](https://www.balena.io/etcher/)

## Turn On
- Install SD Card
- Plug in an HMDI monitor before powering on
- Power using a compatible USB-C adapter. There is a bug with the RPI 4's USB-C power plug design, so be careful to use not just any adapter. There are cheap adapters out there.
- Plug in a USB Keyboard

## Configure PI
On first boot, the PI should resize the volume to match the card size

- login: `pi`
- password: `raspberry`

Note: on French keyboards `q` and `a` keys will be inverted. We'll fix keyboard configuration in next steps
  
Tip: if you can't see your command line because of overscan, once you are logged in type `clear` and `{enter}` a few times. We'll fix over/underscan in next steps.

When you get to the command line, open `sudo raspi-config` to start configuring your installation

### Keyboard
In this order of frequency, I use: French, Swiss French, American, Korean, Chinese, Japanese, Swiss German, and a whole bunch of other keyboards (my students are from everywhere). Here is how I set up my French keyboards:

- `5` Localisation Options > `L3` Keyboard > `Generic 105-Key` (or whatever) > `other` > `French` > Keyboard layout `French` > `default` > `no compose key`

### Wifi
- `1` System > `S1` Wireless LAN > configure your wifi

### Password
- `1` System > `S3` Password > enter a unique password

### Autologin
- `1` System > `S5` Boot/Auto-login > `B2` Console Autologin (or `B1` if you want to stay safe)

### Camera
- `3` Interface > `P1` Camera > `YES`

### SSH
- `3` Interface > `P2` SSH > `YES` (make sure you set a good password)

### SPI
- `3` Interface > `P4` SPI > `YES` (if you do electronic interfaciung stuff over SPI)

### I2C
- `3` Interface > `P5` SPI > `YES` (if you do electronic interfaciung stuff over I2C)

### Display
- `2` Display Options > `D2` Underscan > `YES/NO` (depending on your monitor's handling of the HDMI signal)

`Finish` to exit this menu to the command line

### Overscan Problems
If you're still having problems with overscan, from the command line, open the editor of the configuration file :
`sudo nano /boot/config.txt`. Remove `#` symbols to make sure `#disable_overscan=0` (yes, this is the de-activation of a negative, yes all this is impossibly inelegant) and un-comment to change values of `overscan_left=40`, etc. I have sometimes used negative values in the past. More recent monitors do not usually need overscan and as you can `disable_overscan=1`.

Quit the `nano` text editor by typing the `{ctrl}` + `x` keys > `y` + `{enter}`. And then reboot from the command line with `sudo reboot now`. You might need to `clear` and `{enter}` to see your command prompt.

## Bluetooth Keyboard
I like using the Logitech K380 keyboards because they allow easy switching between various devices: PI, Mac, PC, iPad, etc. They come in pink, as well as other, less important, colors. They (finally) have all the colors in the French keyboard layout: [https://www.logitech.com/fr-ch/product/multi-device-keyboard-k380?crid=27](). These are very handy in complex art installations that often make it difficult to access the ports. 

To pair a bluetooth keyboard, you need put your keyboard into pairing mode, then to go into `bluetoothctl`, `scan` the bluetooth controller for available bluetooth devices identifiers, find your device, turn off scan, and then `pair`, `trust`, and `connect` your device.

During the Logitech keyboard `pair` process you need to enter a `######` + `{enter}` keyboard combination that is random each time. Follow the instructions from the command line.

```
sudo bluetoothctl
[bluetooth]# power on
[bluetooth]# agent on
[bluetooth]# default-agent
[bluetooth]# scan on
[bluetooth]# scan off
[bluetooth]# pair XX:XX:XX:XX:XX
[bluetooth]# trust XX:XX:XX:XX:XX
[bluetooth]# connect XX:XX:XX:XX:XX
[bluetooth]# exit
```

## Connect Via SSH
To control your Raspberry from your Mac, Windows or Linux computer, find your Raspberry's IP address by typing `ifconfig` on the command line of the Raspberry Pi. You'll find your Ethernet, localhost, and Wifi addresses listed as `inet 192.168.#.###` with actual numbers instead of `###`.

For example, on a Mac, open the **Terminal** (`{command}` + `{space}` + `Terminal`) and connect via SSH:

```
ssh pi@192.168.#.###
```

Enter the `password` of the Raspberry Pi and you are now controlling the PI from the Terminal of your personal computer. This is easier for some commands, for example the long list of `CMAKE` commands below.

If you have an error similar to `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` you might need to remove your IP address from the "known hosts" file. To remove my "known hosts" file I remove the line containing the offending IP address from VS Code on my Mac:

```
code /Users/abstractmachine/.ssh/known_hosts
```

## Update
```
sudo apt-get update
sudo apt-get upgrade
```

## Install OpenCV
This suite of commands is entirely based on the Q-Engineering OpenCV Installation guides: [https://qengineering.eu/install-opencv-4.5-on-raspberry-pi-4.html](). These guides are amazingly detailed with information that I will not reproduce here.

### Check eprom update
```
# to get the current status
$ sudo rpi-eeprom-update
# if needed, to update the firmware
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

### Dependencies
Many of following installations are also installed [via openFrameworks](https://github.com/openframeworks/openFrameworks/blob/master/scripts/linux/debian/install_dependencies.sh), but since there is not a 100% overlap, I do all these first.

There are a lot of of `Y`es prompts, so you have to watch the output.

```
$ sudo apt-get install cmake gfortran
$ sudo apt-get install libjpeg-dev libtiff-dev libgif-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
$ sudo apt-get install libgtk2.0-dev libcanberra-gtk*
$ sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
$ sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev
$ sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev libv4l-dev
$ sudo apt-get install libopenblas-dev libatlas-base-dev libblas-dev
$ sudo apt-get install libjasper-dev liblapack-dev libhdf5-dev
$ sudo apt-get install protobuf-compiler
```

### OpenCV
I am currently using `4.5.2`. Check for latest releases on [https://github.com/opencv]().

Note: `-O` is the letter `O` for [`--output-document`](https://www.gnu.org/software/wget/manual/wget.html#Download-Options) and not the number zero.

```
$ cd ~
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/4.5.2.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.5.2.zip

$ unzip opencv.zip
$ unzip opencv_contrib.zip

$ rm opencv.zip
$ rm opencv_contrib.zip

$ mv opencv-4.5.2 opencv
$ mv opencv_contrib-4.5.2 opencv_contrib
```

### Python
Since we're on a Raspberry that will probably be single-use, I'm not installing a virtual environment. This is a bad idea on a personal computer that you use for multiple projects.

We need to install `pip`, because it isn't installed on "Lite" versions of Raspberry OS.

```
$ sudo apt-get install python-pip
$ pip install numpy
$ export PATH=/home/pi/.local/bin:$PATH
```

### Make

```
$ cd ~/opencv/
$ mkdir build
$ cd build
```

```
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
-D ENABLE_NEON=ON \
-D ENABLE_VFPV3=ON \
-D WITH_OPENMP=ON \
-D WITH_OPENCL=OFF \
-D BUILD_TIFF=ON \
-D WITH_FFMPEG=ON \
-D WITH_TBB=ON \
-D BUILD_TBB=ON \
-D BUILD_TESTS=OFF \
-D WITH_EIGEN=OFF \
-D WITH_GSTREAMER=ON \
-D WITH_V4L=ON \
-D WITH_LIBV4L=ON \
-D WITH_VTK=OFF \
-D WITH_QT=OFF \
-D OPENCV_ENABLE_NONFREE=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D BUILD_opencv_python3=TRUE \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D BUILD_EXAMPLES=OFF ..
```

Make sure to include the `..` at the end.

Increase the `swapfile` settings temporarily:

```
sudo nano /etc/dphys-swapfile
```

Change this line
```
#CONF_SWAPSIZE 100
CONF_SWAPSIZE 2048
```

Leave `nano` with `{ctrl}` + `x` > `Y` + `{enter}`.

From the command line, restart the swapfile service thingamajig with this new value:

```
$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start
```

Now we can finally make our build:

```
$ make -j4
```

And now that we've built it, install it:

```
$ sudo make install
$ sudo ldconfig
# cleaning (frees 300 KB)
$ make clean
$ sudo apt-get update
```

Reset the `swapsize` back to its standard value :
```
$ sudo nano /etc/dphys-swapfile
```

```
CONF_SWAPSIZE 100
#CONF_SWAPSIZE 2048
```

Reboot:
```
$ sudo reboot
```

### Verify Installation

```
python
```

```
>>> import cv2
>>> cv2.__version__
'4.5.2'
>>> print( cv2.getBuildInformation() )
>>> quit()
```

```
python3
```

```
>>> import cv2
>>> cv2.__version__
'4.5.2'
>>> print( cv2.getBuildInformation() )
>>> quit()
```
