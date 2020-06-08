# Intelligent-Auto

![logo](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/IA_logo.png)

Intelligent-Auto is a Qt-based infotainment center for your current Linux OpenAuto installation!
Main features include:

*	Embedded OpenAuto `Windowed/Fullscreen`
*	Wireless OpenAuto Capability
*	On-screen Volume Control
*	Responsive Scalable UI `Adjusts to any screen size`
*	Bluetooth Media Control
*	Real-Time Vehicle OBD-II Data `Read-Only`
*	Theming `Dark/Light mode` `Selectable Accent Colors (Fire, Azure, Lilac, Jade, Rose, Steel)`
*	True Raspberry Pi 7” Official Touchscreen Brightness Control
*	App-Launcher built in
*	Camera Access `Streaming/Local` `Backup` `Dash`
*	Keyboard Shortcuts `GPIO Triggerable`


![home](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/home.png)

![openauto_maps](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/openauto_maps.png)

![openauto_spotify](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/openauto_spotify.png)

![media](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/media.png)

![data](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/data.png)

![settings](https://github.com/rsjudka/intelligent-auto/blob/master/docs/imgs/settings.png)

# Getting Started

## Prerequisites

The following packages have been used while developing this application.
> **(NOTE some things may be missing and others are not actually needed)**

Install the following packages:
*	alsa-utils
*	cmake
*	libboost-all-dev
*	libusb-1.0.0-dev
*	libssl-dev
*	libprotobuf-dev
*	protobuf-c-compiler
*	protobuf-compiler
*	libqt5multimedia5
*	libqt5multimedia5-plugins
*	libqt5multimediawidgets5
*	qtmultimedia5-dev
*	libqt5bluetooth5
*	libqt5bluetooth5-bin
*	qtconnectivity5-dev
*	pulseaudio
*	librtaudio-dev
*	librtaudio6
*	libkf5bluezqt-dev
*	libtag1-dev
```
sudo apt update
sudo apt install <package>
```
> **NOTE add multiple packages with a single space between**

If you plan on using the Qt video library instead of the OMX library (i.e. not using a Raspberry Pi) you'll also most likely want to install the following packages:

>> **The option to build with the Qt Video Library instead is available when using a Raspberry Pi 3 (or later) or another Linux device:**

*	libgstreamer1.0-0
*	gstreamer1.0-plugins-base
*	gstreamer1.0-plugins-good
*	gstreamer1.0-plugins-bad
*	gstreamer1.0-plugins-ugly
*	gstreamer1.0-libav
*	gstreamer1.0-doc
*	gstreamer1.0-tools
*	gstreamer1.0-x
*	gstreamer1.0-alsa
*	gstreamer1.0-gl
*	gstreamer1.0-gtk3
*	gstreamer1.0-qt5
*	gstreamer1.0-pulseaudio
```
sudo apt install <package>
```
### NOTE add multiple packages with a single space between

Raspberry Pi Specifically
For a Raspberry Pi, you will also need to run the following commands to build the ilclient:
```
cd /opt/vc/src/hello_pi/libs/ilclient
make
```

### Building
Clone the repo with all submodules:
```
cd ~
git clone https://github.com/rsjudka/intelligent-auto
cd intelligent-auto
```
It is assumed you have cloned this repo with all submodules and are in it’s root directory before moving on.  Pay close attention to the next steps as they are split between whether or not a raspberry pi is used.

If NOT on a Raspberry Pi, use the following commands:
```
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ../
make
```
If using a Raspberry Pi, use the following instead:
```
mkdir build
cd build
cmake -DRPI_BUILD=TRUE -DCMAKE_BUILD_TYPE=Release ../
make
```
### Running

Building the IA Dash will create the ```ia``` binary in <build folder>/bin/.  Depending on what you're running it on, you may need to make some adjustments to your system.

Some things to consider when configuring your system:
*	Utilize a desktop environment that supports transparency (consider using XFCE on Raspberry Pi)
*	Set the background color to black and hide any desktop elements (icons, panel, dock, etc.)
*	Set USB permissions (/etc/udev/rules.d/<rules file>)

### Gotchas

### Brightness Control

There are options for which brightness module is utilized.  If you aren’t using the official Raspberry Pi 7” touchscreen, choose the “mocked” option.  In this mode however, adjusting the brightness does not actually change the screens brightness, it only changes the opacity of the window.

### Bluetooth

Authentication of bluetooth connections are not handled in the application (i.e. the first time you are connecting a device). To keep things simple, you could install a package like ```blueman``` which will prompt you for the necessary actions. If you are still having problems, you may need to try manually authenticating the bluetooth connection.

### OBD-II

There is currently no option for setting the OBD-II interface. Currently it is assumed that an adapter is connected on /dev/ttyUSB0.
Settings are saved periodically every 10 seconds (or anytime the save button is clicked).
Not all OpenAuto settings are accessible.

### GStreamer

If using GStreamer for your video backend, you may get some black bars around the margins of OpenAuto. I'm still trying to figure out a way for it to ignore the aspect ratio.


### Future Features/Enhancements (in no particular order)

*	Radio player (UI elements exist, just haven't had anything to interface with yet)
*	Support Bluetooth OBD-II/CANBUS adapter
*	Wireless hotspot controls
*	Modular OBD-II Data & Error Code tabs
*	Automatic Light/Dark mode (RTC capabilites)
*	Audio Equalizer
*	dashcam video tab
*	Ignore apsect ratio of OpenAuto for GStreamer backend

