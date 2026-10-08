---
title: "The atonement : gnome-launch-box"
pubDate: "2010-09-20T17:45:38.000Z"
description: "Set up GNOME Launch Box as a Mono-free launcher on Fedora, with a custom Compiz keyboard shortcut."
---
Seriously, It was an embarrassing moment when I had to deal with the comments in my [previous post](https://antonakoglou.com/2010/09/13/gnome-do/) as all I wanted to do is give people some piece of info on how to make their life easier using gnome-do. What I didn’t notice was that gnome-do is written in Mono (which I don’t dislike as it is hard for me to disapprove).

**[Carl van Tonder](http://supervacuo.com/)** suggested gnome-launch-box and yes I had to give it a try and I did. So either go to Add/Remove Software (I use Fedora 13), or go to the terminal and type or copy/paste : su -c “yum install -y gnome-launch-box”

now you have installed gnome-launch-box. What is next, is to create a short-cut with your compositing window manager (I have compiz fusion). Go to the settings manager of compiz and then at General -> Commands. At the “Commands” tab go to “command line 0” (or whatever you want) type gnome-launch-box. Then go to the “Key bindings” tab and at Run command 0 (or whatever number you previously chose) enable it and then create the short-cut you wish. And now we are done!

\==In Greek/Στα ελληνικά==

Ώρα για την εξιλέωση! Αφού το gnome-do είναι λίγο ευαίσθητο από νομικής άποψης (λόγω του Mono) και δεν θέλουμε τέτοιους μπελάδες στο pc μας, προτείνω λοιπόν το gnome-launch-box.  Μπορούμε πολύ εύκολα μέσω του Add/Remove Software, γράφωντας το όνομα (με τις παύλες) ή μέσω του τερματικού (su -c “yum install -y gnome-launch-box”) να εγκαταστήσουμε το πρόγραμμα.

Για να το λειτουργήσουμε εύκολα όπως και το gnome-do μπορούμε να δημιουργήσουμε μια συντόμευση πληκτρολογίου για να το καλούμε όποτε θέλουμε. Εγώ χρησιμοποιώ το compiz fusion. Στο settings manager του compiz πάμε στο General -> Commands. Έπειτα στην καρτέλα “Commands” πάμε στο “command line 0” (ή σε όποιο νουμεράκι επιθυμούμε) και γράφουμε την εντολή gnome-launch-box. Στην διπλανή καρτέλα “Key bindings” επιλέγουμε το “run command 0” (ή το νουμερο που επιλέξαμε πριν), ενεργοποιούμε και δημιουργούμε την συντόμευση που θέλουμε. Και είμαστε έτοιμοι!
