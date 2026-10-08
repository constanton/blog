---
title: "MSP430 + Eclipse CDT on Fedora 19"
pubDate: "2013-08-31T20:50:23.000Z"
description: "Configure Eclipse CDT and MSP430 tools on Fedora 19 to build and flash a blinking-LED project."
---
Hello! This is a guide to install Eclipse and everything required to flash your project to a MSP430 board 🙂

First, you need to install Eclipse CDT (the Eclipse version using the C/C++ IDE) and there are three ways:

1.  Go the Eclipse’s website, download and install it yourself
2.  Use Fedora’s “Software” application (which is PackageKit, the GUI of yum) and search for “eclipse-cdt”
3.  Use your terminal, type su, press enter, give your root password and then type yum install eclipse-cdt. Type “y” to install all dependencies required for eclipse-cdt 🙂

After you have successfully installed Eclipse CDT you can continue to the main course. We need a plugin for MSP430 called [msp430-eclipse by xPG](http://xpg.dk/projects/msp430/msp430-eclipse/ "MSP430 xPG pluggin for Eclipse"). Don’t download anything yet. We’ll use Eclipse for that!

Now, open Eclipse go to _Help->Install_ new software and add **[http://eclipse.xpg.dk](http://eclipse.xpg.dk)** as a software source. Use it to install the _msp430_ plugin.

Next, we need a tool-chain that includes all files to compile, debug etc our code specifically for our MSP430 platform! Visit [xPG’s website](http://xpg.dk/projects/msp430/msp430-eclipse/) as mentioned previously. Scroll down and choose the version of the tool-chain for your system.

We will need to install a few packages more though as xPG’s tool-chain is not sufficient (If you try to compile without those packages it will fail to find libmpc.so.2, or something like that). I fixed it by installing five msp430-related packages: msp430-binutils, msp430-gcc, msp430-libc, msp430mcu, mspdebug. Maybe some of them are not really needed but ok it’s only a few Kbytes and in the end everything works well. You can use step 2 or step 3 from above!

_If you are confident for your tool-chain and skipped my previous steps, you don’t need to download any package (the next step), you just need to configure Eclipse later on._

Download and extract the package in an appropriate location (like your home folder, or any other folder inside it). Go to Eclipse (with the plugin already installed, like I showed you before) and from Eclipse’s menu click on _MSP430 -> Tool Manager_. Press  “Add…”, find the tool-package folder, select it and click OK. On the _Tool Manager_, select the tool-chain and press “Activate”.

If you want to use your own tool-chain, all MSP430 compilation and debug tools can be configured at _Window->Preferences->MSP430_.

As normal users we don’t have permission to use the USB bus. To fix that, go to Fedora’s “Users and Groups” or system-config-users (if you don’t have that install it like all other packages). Create a group named eg. “usb” and add your user into it (“Users” tab -> select your user-> Properties). Log out and log in again for changes to take effect.

Next, go to a terminal, type “su -” and create a file with the command: gedit /etc/udev/rules.d/71-persistent-msp430.rules . Then, copy, paste and save this:

> SUBSYSTEM==”usb”, ATTRS{idVendor}==”0451″, ATTRS{idProduct}==”f432″, MODE=”0660″, GROUP=”usb”

The numbers “0451” and “f432” can be verified if you connect your board and use the command “lsusb”.  Now, go to a terminal for the last time and give these three commands:

> systemctl restart systemd-udevd.service
> 
> systemctl restart systemd-udev-trigger.service
> 
> systemctl restart systemd-udev-settle.service

Now, let’s make a new project and test what we’ve done. This will require a MSP430 board, hopefully supported by the plugin (which is very probable as you will notice). Create a new C/C++ project and select the “Empty project” at the “MSP430 Cross Target Application” folder. Give it a name and then click Finish.

Right-click the project at the “Project Explorer” and choose Properties. Go to the “MSP430” section, select your MCU and debug settings. Next, go to the “C/C++ General” section -> Paths and Symbols, select GNU C at the “Includes” tab and include the path “/home/_**username**/**any\_directory**_/msp430-toolchain-linux-amd64-3.0/msp430/include” (same for GNU C++)

Right-click the folder, create a src folder and place a source file into it preferably with a blink.c (a blinking LED example) file for your board such as this one in this blog. Don’t forget to include your board’s header file!

Build the project, then right-click the project and select _MSP430->Upload to target_ (or use the icon for that job at the main bar).

The example should work and this brings us to the end of this tutorial 🙂
