---
title: "Disable NVIDIA on Sony VAIO VPCZ11X9E (Fedora 17) and more news"
pubDate: "2012-07-26T12:56:09.000Z"
description: "Disabling a Sony VAIO's NVIDIA GPU on Fedora 17 to reduce heat and battery drain."
---
Hey! I know I haven’t posted anything these past few months but I would have no excuse if I didn’t post about that: I have disabled my NVIDIA card from the “Dynamic Hybrid Graphics System” of my Sony VAIO VPCZ11X9E.

A few more news: 2nd semester on my post-grad program was even better than the 1st one. Plus, the band I am participating in (both playing and composing), named [Wonky Doll and the Echo](http://wonkydollandtheecho.com/ "Wonky Doll and the Echo website"), is about to release it’s debut album! Feel free to listen to four of our songs on [SoundCloud](http://soundcloud.com/wonky-doll-and-the-echo "Wonky Doll and the Echo") (even more links there 🙂 )

Now, back to modifying our system, why would I want to disable my NVIDIA card? It’s because what I can only get out of this “hybrid system” is only the performance of my Intel card at the cost of Intel **+** NVIDIA working together! That means, more heat and faster battery discharges! Oh, by the way, I am now using Fedora 17 which is a lot more stable than Fedora 16 I must say (thanks GNOME!).

What I need to tell you is that: If you don’t know what you are doing, don’t trust any guide like this (…or do things at your own risk) 🙂 But you should know that in case of failure of this procedure, if you have at least once updated your kernel, you can just go back to the previous one and delete the files we will create. This will solve most of the crashes that might happen if you don’t follow the instructions correctly.

The [Bumblebee](http://bumblebee-project.org/) project is for resolving the NVIDIA Optimus problem, not SONY’s hybrid system installed on some VAIO’s. So, I didn’t try that. What we are going to use is  [**acpi\_call**](https://github.com/mkottman/acpi_call/ "acpi_call") which is a kernel module (tip: that means it needs to be compiled again after a kernel update 🙂 )that will help us configure Fedora”s power management system in order to shut down the NVIDIA card.

My resources in order to learn how to shut down the card were mainly these:  
[http://amolh.weebly.com/2/post/2012/02/asusu36sd.html](http://amolh.weebly.com/2/post/2012/02/asusu36sd.html)  
[http://hybrid-graphics-linux.tuxfamily.org/index.php?title=ACPI\_calls](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=ACPI_calls)

We first need (as root) to download (lines 1-3), get inside the folder (line 4), compile (line 5, for that you need gcc, kernel-headers etc. if you don’t know what all that is…ask someone!), install the module on the current kernel  (lines 6-8) and test if it worked (that means the output of test\_off.sh should get you one “works” next to a ACPI handle :

**\# yum -y update**  
**\# yum install git**  
**\# git clone [https://github.com/mkottman/acpi\_call](https://github.com/mkottman/acpi_call)**  
**\# cd acpi\_call**  
**\# make**  
**\# cp acpi\_call.ko /lib/modules/\`uname -r\`/kernel/drivers/acpi**  
**\# depmod -a**  
**\# modprobe acpi\_call**  
**\# chmod +x ./test\_off.sh**

I got this one: **Trying \\\_SB.PCI0.P0P2.DGPU.\_OFF: works!** …which is great!

The result of the script will also be an increase of the battery duration (which I haven’t tested yet as my battery died a few months ago) and a decrease in the temperature of your system (you can see that in your terminal if you install the [lm\_sensors](http://lm-sensors.org/) package on “Add/Remove Software” or “yum install lm\_sensors”. The temprature of the NVIDIA card will drop to -1 degrees Celsious. The temprature of my CPU dropped approx. from 70 to 58 degrees!!!  
Now you are able to shut down the NVIDIA card manually while you are using Fedora. Next, we have to make Fedora do this automatically in every boot.

As “su -” we will create a script named nvidia\_off.sh :

# **gedit  /usr/local/bin/nvidia\_off.sh**

and inside this script you will paste this:

> #!/bin/sh  
> echo “——————————-” >> /var/log/nvidia.log  
> echo \`date\` >> /var/log/nvidia.log  
> echo “Disabling Nvidia video adapter !! ” >> /var/log/nvidia.log  
> echo “——————————-” >> /var/log/nvidia.log  
> echo “\\\_SB.PCI0.P0P2.DGPU.\_OFF” > /proc/acpi/call

What’s important is the first and the last line only. The last line might need modification from your part as the ACPI handler might be different for your system (if you have a different laptop than mine). The other lines are not compulsory. Since I use an SSD disc and have moved my /var/log folder in RAM that means logging this info is not really of value. But for everyone else who hasn’t done this it’s cool for debugging.

Now we need to modify the priviledges of this script with:

**\# chmod 775 /usr/local/bin/nvidia\_off.sh**

Next step is to configure our system to load the acpi\_call module we installed in each boot. For that purpose we create a .conf file here (again with su -):

**\# gedit /etc/modules-load.d/acpi\_call.conf**

and just write or paste just this : **acpi\_call**

Since we now know that our module will be loaded it is safe to execute our “nvidia\_off.sh” script.

To do that we need to create another script in /etc/rc.d/ named “rc.local” (it used to exist in previous releases, now it doesn’t):

**\# gedit /etc/rc.d/rc.local**

and write down  or copy-paste this:

> #!/bin/bash  
> /usr/bin/sh /usr/local/bin/nvidia\_off.sh

The final step is to stop the nouveau driver get activated during startup, as it will crash your system. We need to edit grub2:

**\# gedit /boot/grub2/grub.cfg**

in this file you must be able to recognise the kernel in which you have just installed acpi\_call next to the word _menuentry_ 🙂 if you are not sure what’s your current kernel just use the command “uname -r”.

Now, right before the word quiet (which is before the command “echo ‘Loading initial ramdisk …’ “) paste this:

> rdblacklist=nouveau

Yes, it blacklists the nouveau driver so that it will not load. If you boot succesfuly you will notice that the temprature of the NVIDIA card will not be mentioned anymore but the significant temprature drop will still be there. 🙂
