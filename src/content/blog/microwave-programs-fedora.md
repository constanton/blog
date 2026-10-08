---
title: "Microwave circuit design/sim programs on Fedora"
pubDate: "2011-01-10T12:14:00.000Z"
description: "Setting up microwave circuit design and simulation tools on Fedora, including Qucs and Meep."
---
Hello once more,

Recently I made a presentation at the TEI of Pireaus on Arduino and Fedora Electronic Lab. Hopefully, I will repeat it to give the chance to more people to come.

I intend to make some simple tutorials (we’ll see how complex they’ll get on the way actually) on using programs that assist or create designs and simulations of microwave circuits and set-ups. In this post, I will just post a simple guide to install some programs that deal with the design and simulation of microwave circuits and components. What I am trying to do is at least reach the 3D FDTD simulation using free and open source software. Currently I have found [Qucs](http://qucs.sourceforge.net/screenshots.html "qucs screenshots"), [Transcalc](http://transcalc.sourceforge.net/), [emGine](http://www.petr-lorenz.com/emgine/) and MIT’s [Meep](http://ab-initio.mit.edu/wiki/index.php/Meep) that will help us reach this goal. I am trying to install [Elmer-FEM](http://www.csc.fi/english/pages/elmer) (which looks extremely cool and a lot easier than Meep) but unfortunately, I couldn’t install it due to problems with a certain dependency (ftgl-devel is installed but not found 😦  [see here](http://forums.fedoraforum.org/showthread.php?t=257027)).

You can easily install [Qucs](http://qucs.sourceforge.net/) with : $ su -c “yum install qucs” (it’s also inside [Fedora Electronic Lab](http://spins.fedoraproject.org/fel/) together with other valuable packages). It’s a circuit simulation program (not only for microwave circuits) that has various microwave components to use.

[Transcalc](http://transcalc.sourceforge.net/) is ” an analysis and synthesis tool for calculating the electrical and physical properties of different kinds of RF and microwave transmission lines”. The idea behind this is to get the dimensions of real components and then use the results (the parameters we need) in our simulation programs!

To install Transcalc you will need to install the GTK2.0 development files (gtk2-devel on fedora). After you [download the package](http://transcalc.sourceforge.net/#download) and place it in a folder of your choice (I have a “programs” folder and place every to-be-installed program there) you can go to the terminal and write :

> $ cd ./your\_path\_to\_transcalc\_folder/
> 
> $ ./configure (if something is missing search in yum or “Add/Remove applications”)
> 
> $ make
> 
> $ su -c “make install” ….and to run the program just type : $ transcalc

A few words for [emGine](http://www.petr-lorenz.com/emgine/index.php)! It’s a full-wave 3D electromagnetic field simulation environment solving Maxwell’s equations in time-domain. You create 3D models of your components, put the parameters and then simulate and get your graphs and results. Not 3D FDTD.

Let’s install it then! You are going to need to find and install (if not already installed): tkinter , python, vtk , vtk-devel, wxWidgets (I got wxBase, wxGTK, wxGTK-gl, wxGTK-media installed) , wxPython, numpy and python-matplotlib. Now go to the [download page](http://www.petr-lorenz.com/emgine/index.php?option=com_content&view=article&id=45&Itemid=55) and get the package (emGine GUI platform independent of course) .

As you understand we are going to compile using python. So, go to the emGine folder (like we did in transcalc) and just type in your terminal:

> $ python emGine.py

It might take a bit to run, but if nothing is missing the program shoud start. And that’s for the emGine environment.

Now, to the more serious staff. [Meep](http://ab-initio.mit.edu/wiki/index.php/Meep) is an FDTD program to model electromagnetic systems! One of my next posts will be an example running a 3D (I hope) simulation (if not a 3D then a 2D). I will try to get the dimensions of a real waveguide, get the parameters from Transcalc, use them on Meep to visualize a cool simulation and maybe see what we can do on a circuit with Qucs.

What did I need to install Meep on Fedora 14?

[libctl](http://ab-initio.mit.edu/wiki/index.php/Libctl) (new version on the link, or install libctl and libctl-devel version 3.0.2 from yum etc.), hdf5 and hdf5-devel. I think that was all I needed.

Then let’s go to the terminal one last time:

> $ export LDFLAGS=”$LDFLAGS -lm”    (this line is needed to avoid the [DSO Linking error](http://fedoraproject.org/wiki/UnderstandingDSOLinkChange) with libm.so)  
> $ make  
> $ make install

Now if you type: $ meep …you should get:  meep>    I tried to make a 2D example to simulate a waveguide. Not the fastest thing I have done in my life 😛

The [reference](http://ab-initio.mit.edu/wiki/index.php/Meep_Reference) is here. Start the calculations and wait for my 2nd post. (Also, just found it, check [this](http://foac.sourceforge.net/?page_id=12) out, there are tools like the japanese [ADVENTURE](http://adventure.sys.t.u-tokyo.ac.jp/project/) and its modules)
