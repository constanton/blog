---
title: "Sound fix for Adobe Flash for Firefox 4 beta on Fedora"
pubDate: "2011-02-19T18:37:21.000Z"
description: "A compiled memcpy workaround for Adobe Flash audio problems in Firefox 4 beta on 64-bit Fedora 14."
---
I am currently using Firefox Minefield 4.0b12pre but I have tried this fix also on Firefox 4 beta 11 on my 64 bit system (Fedora 14)! This problem has occured to me with the 64 bit Adobe Flash plugin 10.2.

Some of the code I will paste here (the code for creating the linusmemcpy.c file)  was found in this [post](http://ahabdo.wordpress.com/2011/01/03/flash-64-bit-crappy-sound-fix-for-fedora-14/ "Ahmed Abdo's fix") at Ahmed Abdo’s blog!

I will give you the script code to paste it in the terminal as after doing some trivial staf f the bug will be exterminated! But I will pretty much explain what this script does.

In general, what we need to do is to create a C file (with a certain memcopy function that will solve our problem) , and the binary and then load the binary when we open Firefox.  The first line of the script creates our C file at the hidden folder .mozilla  (to unhide use Control+H) named linusmemcpy.c , then “cat” is waiting for us to write our text (this time the C code) until we write EOF (end of file). Then what we do is to enter the .mozilla folder and compile the c file. Our last step is to use the GNU Linker with ld on the binary files.

Just copy the whole text and paste it on your terminal as it is 🙂

> ```
> cat > $HOME/.mozilla/linusmemcpy.c <<EOF
> #include <sys/types.h>
> 
> void *memcpy(void *dst, const void *src, size_t size)
> {
> void *orig = dst;
> asm volatile("rep ; movsq"
> :"=D" (dst), "=S" (src)
> :"0" (dst), "1" (src), "c" (size >> 3)
> :"memory");
> asm volatile("rep ; movsb"
> :"=D" (dst), "=S" (src)
> :"0" (dst), "1" (src), "c" (size & 7)
> :"memory");
> return orig;
> }
> EOF
> cd $HOME/.mozilla/
> gcc -O2 -c linusmemcpy.c
> ld -G linusmemcpy.o -o linusmemcpy.so
> ```

```
linusmemcpy.clin
```

Now the next very small step is to automate the procedure of starting Firefox correctly with the shortcut on the desktop panel. We will create a small shell script the same way we did with our C file. If you are using beta that means somewhere in your system exists the “firefox” shell script that executes the firefox-bin. We need to know the path to it! If already have a shortcut, right click -> Properties and look at “Command” . This is it. Mine (for [firefox 4](http://fedoraproject.org/wiki/Firefox_4) from spot’s repos) says firefox4. Don’t forget the & at the end 😉

> cat > $HOME/.mozilla/custom\_firefox\_startup.sh <<EOF  
> LD\_PRELOAD=$HOME/.mozilla/linusmemcpy.so firefox4 &  
> EOF  
> chmod u+x $HOME/.mozilla/custom\_firefox\_startup.sh

So, now is our last step! Go to the icon of Firefox on the desktop panel , right click -> Properties , and at the command click “Browse” press control+H to unhide the folders, enter the .mozilla folder and select “custom\_firefox\_startup.sh”.

Now, close every instance of Firefox that is running right now (yes I ask too much, but you can leave my blog 🙂 ) and press the Firefox button 🙂

\==== Ελληνικά/Greek ====

Σε αυτό το post δίνω οδηγίες για το πως να φτιάξετε το πρόβλημα που έχει παρουσιαστεί με τον ήχο στο Flash της Adobe (10.2) για τον Firefox 4 beta 11 (αυτό και το Minefield στην έκδοση 4.0b12pre δοκίμασα, λογικά τρέχει και σε άλλες beta). Χρησιμοποιό την 64bit εκδοση του Fedora 14.

Θα εξηγήσω λίγο τι γινεται με το script, όμως μπορείτε να το αντιγράψετε και να το επικολλήσετε στο terminal ολόκληρο χωρίς να γράψετε τίποτα εσείς! Απλά τα γράφω για να μη τα κάνετε απλά copy paste χωρίς να ξέρετε τί γίνεται περίπου.

Στη πρώτη εντολή δημιουργούμε ένα κενό αρχείο που θα είναι o C κώδικας με το fix μας (μια συνάρτηση που λέγεται memcpy) στο οποίο θα γράψουμε ότι χρειάζεται και θα περιμένει την λέξη EOF (που σημαίνει τέλος του αρχείου , end of file). Μετά δίνουμε την εντολή cd και μας κατευθήνει στον φάκελο .mozilla (η τελεία δίνει είναι κρυφός φάκελος που βρίσκεται στο home folder και για να τον δούμε πατάμε control+H). Εκεί βρίσκονται οι ρυθμίσεις του Firefox. Κάνουμε compile το C αρχείο και εκτελούμε και την εντολή ld για τον GNU Linker.

Στο επόμενο βήμα δημιουργούμε ένα μικρό shell script το οποίο απλά θα προφορτώσει τo binary αρχείο που φτιάξαμε προηγουμένως την ώρα που ανοίγει ο Firefox! Πάμε λοιπόν μετά στο εικονίδιο του Firefox στη μπάρα στην επιφάνεια εργασίας και κάνουμε δεξί click. Στην 3η σειρά με τη λέξη “Command” επιλέγουμε το Browse και από το Home folder πηγαίνουμε στο φάκελο “.mozilla” και επιλέγουμε το custom\_firefox\_startup.sh. Κλείνουμε κάθε παράθυρο του Firefox που είναι ανοιχτό και ξανανοίγουμε. Έτοιμοι! 🙂
