Intro
=====

CRT Notes:
This application was fixed to compile and run on the latest arm versions.
This should work on all new android devices wit a usb host port.

This is a fork from the marcv81's proxdroid project. It was compiled with the version 2.3.0 of the official proxmark3 repo.

This is the proxmark3 client for Android. You'll need a proxmark3 board, a rooted Android device that supports the USB host mode, and a USB OTG cable to connect them. If your Android device does not power the proxmark3 board you may need an external power supply and a Y USB cable.


Build
=====

Install the Android SDK and NDK.
Get the source from GitHub:
  git clone https://github.com/FonkyCorp/proxdroid.git proxdroid
  cd proxdroid
  git submodule init
  git submodule update
Run "ndk-build".

Install
=======

Connect your Android device with "adb connect" and run "install.sh".

Run
===

On the Android device run the Terminal Emulator, execute the command "su", then execute the command "proxmark3 /dev/ttyACM0".

