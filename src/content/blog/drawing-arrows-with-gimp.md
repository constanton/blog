---
title: "Drawing arrows with GIMP"
pubDate: "2010-09-02T09:26:16.000Z"
description: "Install a GIMP script and use paths to add arrows to photos and technical illustrations."
---
Today I desperately needed to draw arrows in a picture to point parts of an Arduino stack with an Ethernet and Xbee shield.

So, I took the picture of the stack, increased the contrast and made other adjustments to perfect the pictures, and I was ready to place the arrows. Arrows? How? OK, I googled and found this [http://registry.gimp.org/node/20269](http://registry.gimp.org/node/20269)

You just have to download the .scm file. If you are a Linux user (obviously I use Fedora), go to your Home Folder and press Control+H to unhide the hidden folders. Next, go to the “.gimp-2.6” (1st: Yes there is a full stop, 2nd: 2.6 is the name of the folder right now according to GIMP’s current version). Inside this folder find the folder “scripts” and place there the .scm file. Now, open GIMP (or re-open if already running), go to Tools and you are good to go 🙂

(Tip: To draw an arrow you must use the path tool at the toolbox. Just click one time to point the start of the arrow and a second time to point the end. You will just make a straight line that will be used as a path)

In Greek : Στον σύνδεσμο που υπάρχει παραπάνω μπορείτε να κατεβάσετε το .scm αρχείο που θα σας επιτρέψει να σχεδιάζετε βέλη με το GIMP αυτόματα. Για να λειτουργήσει το αυτό το script πηγαίνουμε στο Home Folder, πατάμε Control+H για να αποκαλυφθούν οι κρυφοί φάκελοι και στη συνέχεια πηγαίνουμε στον φάκελο “.gimp-2.6″ (1ον ναι υπάρχει τελεία, 2ον το όνομα προέρχεται από την τωρινή έκδοση”). Μέσα σε αυτόν τον φάκελο υπάρχει ο φάκελος “scripts” όπου και τοποθετούμε το .scm αρχείο. Ανοίγωντας το GIMP τώρα μπορούμε να δούμε στο Tools το Arrow 🙂

(Συμβουλή: Για να φτιάξετε το arrow πρέπει να σχηματίσεται ένα μονοπάτι με το path tool. Αν απλά κάνετε ένα κλικ για την αρχή και άλλο ένα για το τέλος του βέλους εκεί που επιθυμείτε είστε έτοιμοι να φτιάξετε το βέλος με το Arrow που βρίσκεται στα Tools)
