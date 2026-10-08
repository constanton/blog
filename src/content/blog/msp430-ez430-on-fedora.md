---
title: "MSP430 (ez430) on Fedora"
pubDate: "2010-10-12T10:27:12.000Z"
description: "Program and debug an ez430 MSP430 development board using Fedora's command-line tools."
---
For learning purposes I currently have on my hands a EZ430-F2013 Development Kit (We all should also use Arduino 🙂 ). This kit comes with a CD containing proprietary software (an IDE) in order to program and debug the MSP430 microcontroller. So, I took the chance to run it on Fedora using Linux tools and a few resources on the internet. In this post I will write down how you can program and debug your ez430 using Fedora 13 and your terminal.

First, I plugged in the ez430 and opened a terminal (yes we will work only this way for now). Write down lsusb and hit enter. Then you should get some lines containing this one:

_Bus 005 Device 003: ID 0451:f430 Texas Instruments, Inc. MSP-FET430UIF JTAG Tool_

That means that by default your system recognises the device and you can actually communicate with it.

Next, we need our tools! Go to System ->Administration-> Add/Remove Software (or use yum install etc.). The software we need is (actually not sure if everything is needed):

*   latest version of gcc, texinfo, patch, ncurses5-dev, zlib, zlib-dev, libX11-dev, libusb-dev (not only libusb1-dev), libreadline6-dev, msp430-binutils, msp430-gcc, msp430-libc

and also : [mspdebug](http://mspdebug.sourceforge.net/ "mspdebug main page") (the program that actually does the work).To install it manually (in case there is an older version on the repository) download the .tar file create a  folder named “Programs” (in case you don’t have one) on your Home Folder.Then, extract the mspdebug folder there!

With your terminal (you can auto-complete the words in the directory using Tab on your keyboard) :

$ _**cd /home/(your user name on Fedora)/Programs/mspdebug-0.11**_

(now you are in the mspdebug folder with your terminal, the version 0.11 is the current one I use, yours can differ)

$ _**make**_ (this will compile the program)

$ _**su -c “make install”**_ (and give your root password to install it)

(the $ symbol is just to show that you are using different commands in the terminal, don’t copy it)

now you have installed mspdebug! Great!

If you are ready to use the MSP430 you should have a program already written. In case you don’t, get this example (modified by me to get it to compile) that flashes the internal LED of the device:

/\* Blink LED example \*/  
#include <msp430x20x3.h>

/\*\* Delay function. \*\*/  
delay(unsigned int d) {  
int i;  
for (i = 0; i<d; i++) {  
nop();  
}  
}

int main(void) {  
WDTCTL = WDTPW | WDTHOLD;  
P1DIR = 0xFF;  
P1OUT = 0x01;   // THE x IS NOT Copy-Pasted CORRECTLY 🙂

for (;;) {  
P1OUT = ~P1OUT;  
delay(0x4fff);  
}  
}

Create a file named blink.c in a folder of your choice, copy this on the file and then cd on the folder. Now to compile it we need 3 lines (I also changed this to work):

$ _**msp430-gcc -Os -mmcu=msp430x2013 -o led.elf blink.c**_

**$** _**msp430-objdump -DS led.elf > led.lst**_

**$** _**msp430-objcopy -O ihex led.elf  led.hex**_

In order not to do this every single time, you need to run the program, you can create a Makefile based on the one [in this site](http://www.siphec.com/HOWTO/MSP430%20HOWTO/) (it’s inside [this zip file](http://www.siphec.com/HOWTO/MSP430%20HOWTO/leds.zip "Leds example zip file with makefile")).

Next, to run mspdebug in order to flash the program into the MSP430, type :

$ _**mspdebug -d /dev/ttyUSB0 uif**_

(“/dev/ttyUSB0” is of course the ez430 if you don’t have any other device and “uif” the parameter to run it with mspdebug, check the manual for more)

To flash the program you need to type : **prog led.hex** . Notice that it is a command to control mspdebug and not the terminal). If you push Control+D mspdebug will close, the ez430 will reset, start the program and also blinking the LED! 🙂

My resources were 3 posts in this site : [http://bit.ly/deonNa](http://bit.ly/deonNa) I should also mention that I have installed all the [Fedora Electronic Lab](http://spins.fedoraproject.org/fel/ "Fedora Electronic Lab site") packages with: $ **su -c “yum groupinstall “electronic-lab”**
