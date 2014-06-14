sixaxis-android
===============

sixaxis-android is a fork from [QtSixA] [1] to run under Android. 

> ### QtSixA is the Sixaxis Joystick Manager
> It can connect PS3 hardware (Sixaxis/DualShock3 and Keypads) to a Linux-compatible machine.

Moreover, sixaxis-android is patched for [Gasia] [2] (DualShock3 clone) gamepad. Due to the way Bluetooth works under Linux, sixaxis-android requires a rooted device. For a demo, watch this [video] [3].

[1]:http://qtsixa.sourceforge.net/
[2]:https://aur.archlinux.org/packages/qtsixa-gasia/
[3]:http://youtu.be/mwG82zSkvbA

Version
-------

0.9

Compilation
-----------

1. Download [Android NDK] [4].
2. Extract the NDK and extract sixaxis-android in the same folder.
3. Change dir to sixaxis-android/sixad-gasia.
```sh
cd sixaxis-android/sixad-gasia
```
4. Open Makefile and adjust NDK_KIT if needed to point to NDK location relative to Makefile.
```Makefile
NDK_KIT = ../../android-ndk-r9d/
```
5. Run make.
```sh
make
```

[4]:https://developer.android.com/tools/sdk/ndk/index.html

Installation
------------

1. After make succeed, the folder bins will be created.
2. Copy the executable in the bins folder (mainly sixad-bin and sixad-sixaxis) to your Android device. Make sure to copy them to a location where you can run them. For example /system/bin.
3. Pair your DualShock3 controller with you Android device using your Android device Bluetooth MAC address. This step should be ran on a separate machine using a USB cable connected to your DualShock3. The Android device Bluetooth MAC address can be obtained as following:

  1. Turn on Bluetooth.
  2. Go to Settings -> About tablet -> Status -> Bluetooth address.

  The following command should be ran on a Linux machine or even a Linux virtual machine using [VirtualBox] [5] for example where XX:XX:XX:XX:XX:XX is the Bluetooth MAC address of your Android device. For more information look at [Ubuntu sixaxis documentation] [6].
  
  ```sh
  sudo sixpair XX:XX:XX:XX:XX:XX
  ```

4. Turn off Bluetooth on your Android device.
5. For sixaxis-android to work correctly, you need to disable bluez input plugin. You have two option according to your device:
  * Rename /system/lib/bluez-plugin/input.so to anything else.
  ```sh
  mv input.so input.so.orig
  ```
  * Edit /system/etc/bluetooth/main.conf to include the following configuration:
  ```
  DisablePlugins = input
  ```
6. Turn on Bluetooth.
7. Go to the folder where you copied sixad-bin in step 2 and run the following command:
  ```sh
  sixad-bin 1 0 0
  ```
8. Click on PS button on your DualShock3 controller.
9. You will see some output from sixad-bin that confirm that pairing was successful.
10. Open your favorite game and enjoy!

[5]:https://www.virtualbox.org/
[6]:https://help.ubuntu.com/community/Sixaxis

Troubleshooting
---------------

If your game does not detect your controller, try to click on the PS button after starting the game instead of clicking it directly after running sixad-bin.

Limitations
-----------

Currently only Android devices with bluez are supported. Newer Android devices with BlueDroid are not yet supported.

License
-------

GPLv2

