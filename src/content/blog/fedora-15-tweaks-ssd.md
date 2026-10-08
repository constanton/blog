---
title: "My Fedora 15 tweaks for an SSD"
pubDate: "2011-05-29T12:40:15.000Z"
description: "Tuning Fedora for an SSD with TRIM, RAM-backed temporary folders, and filesystem settings."
---
### **_NOTE_: Same things apply even on Fedora 17/18/19 🙂**

\====== In English / Αγγλικά ======

Hello! I am going to share how I tweaked my Linux system using Fedora 15!

I did a bit of searching and found some interesting proposals on how to do it. To be honest there isn’t one specific way of doing it. It depends on how much you love your data, how much you want your SSD to live and of course what’s your hardware (eg. my SSD supports TRIM, I have enabled the RAID option and I have 8 GBs of RAM). In short, what I will do is make the system use the TRIM command (which is essential) and put the temporary folders in RAM.

**tip**: if you have other OSs installed and change to RAID mode (with one ssd it’s like AHCI), they might not work (there are guides to avoid re-installation)…Linux will work though 🙂

One great source was this one \[1\].

First of all, we will use the ext4 filesytem (**no** _swap_ partition for me). There is one thing to know! Writing on your SSD without reason or moving/writing data is harming its life expectancy. SSDs have endurance due to the MLC technology \[2\] (approximately 10.000 writes per memory block \[3\]) which is cheaper, but in the end we also want our SSD to live!

Now, apart from my SSD, I also have my old HDD plugged in my computer. It’s SATA so I didn’t have any other problems to set it up. During the installation process, I created my partitions manually. You know: create some free space and then create new partitions with the appropriate mount points. I used “/” ,obviously for a partition for the root directory, and also “/home” to place my data and program configuration on a different partition (and disc). To store “/home” folder, I used the HDD, just because I want to download stuff and save my media files there! Remember that it’s bad for your SSD writing again and again to it.

After you install Fedora 15, to check if your SSD supports the TRIM command (supposing your disc is  /dev/sda) :

> hdparm -I /dev/sda | grep TRIM

(grep will search and find the lines where the word “TRIM” exists in the output of the command before the “|” symbol)

Now, you must edit the “/etc/fstab” file, it’s the filesystem table.You can create a copy of this file in case you feel it won’t work (but, hey, it will) or something else goes wrong:

> cp /etc/fstab /etc/fstab.bakup

How did I edit it? “su -” , give your password and then “gedit /etc/fstab”. Now, visit the second page \[4\] of the guide at step 2! TRIM command support (if your drive supports it of course) ! You absolutely need to do this! Now that you opened “fstab” you need to add the “discard” parameter next to the defaults parameter for the root directory! As you will see at the link it’s **something like** that:

> `/dev/sda1 / ext4 defaults`

That will change to **something like** that:

> `/dev/sda1 / ext4 **discard**,defaults`

Now, it’s up to you if you want to add one other parameter! Tweaking might mean less reliability and data integrity but that’s why I moved my precious data on my HDD 😉 You can also add the “**noatime**” parameter (just like discard)  and, hey(!), Linus Torvalds also suggests it \[5\]

What’s next? Moving our temporary folders to RAM. I have 8 GBs of RAM and I am not afraid to “use” them! By “temporary folders” I mean “/tmp”, “/var/tmp” and “/var/log”. For that, you need to add three lines (each one for every folder) at the “/etc/fstab” file. It’s step 6 at the guide. One line (for /tmp) will look like this:

> `none /tmp tmpfs defaults 0 0`

Don’t worry about “none” (it’s just a name) it helps the folders stand out so that we will find them easier later. Next thing you can do is to also move the Mozilla Firefox cache there (as proposed in the guide)!

To check if everything is working just run the command “df” and it will show you what are you partitions doing!

OK, how can we optimize our system even more? Disabling journaling of ext4 (making it unable to keep track of data, meaning unreliable). **BUT**! This is as far as I will tweak my SSD. Furethermore, we allready changed “noatime”. I have the life expectancy I need and also a high speed disk, having in mind that I want my data uncorrupted as much as possible.

\[1\] [http://cptl.org/wp/index.php/2010/03/30/tuning-solid-state-drives-in-linux/](http://cptl.org/wp/index.php/2010/03/30/tuning-solid-state-drives-in-linux/)

\[2\] [http://en.wikipedia.org/wiki/Multi-level\_cell](http://en.wikipedia.org/wiki/Multi-level_cell "Wikipedia on MLC")

\[3\] [http://www.laptopmag.com/advice/expert/are-ssds-worth-the-money.aspx?page=3](http://www.laptopmag.com/advice/expert/are-ssds-worth-the-money.aspx?page=3)

\[4\] [http://cptl.org/wp/index.php/2010/03/30/tuning-solid-state-drives-in-linux/2/](http://cptl.org/wp/index.php/2010/03/30/tuning-solid-state-drives-in-linux/2/)

\[5\] [http://kerneltrap.org/node/14148](http://kerneltrap.org/node/14148)

\======= In Greek / Ελληνικά =======

Για να λειτουργήσετε τον SSD σας ώστε να “ζήσει” και να λειτουργεί στην μέγιστη απόδοση, δεν υπάρχει μόνο ένας τρόπος. Ανάλογα με το hardware του υπολογιστή σας (ο δικός μου υποστηρίζει την εντολή TRIM , έχω ενεργοποιήσει το RAID mode και έχω 8GB RAM),και το πόσο χρειάζεστε την ασφάλεια των δεδομένων σας πρέπει να επιλέξετε εσείς τί αλλαγές θα κάνετε. Αυτό που είναι σίγουρο πως πρέπει να κάνετε είναι να ενεργοποιήσετε τη λειτουργεία TRIM του λειτουργικού. Εγώ επέλεξα και να μεταφέρω τους φακέλους “/tmp”, “/var/tmp /” και “/var/log” στη RAM, όπως επίσης εφτιαξα ένα partition για το  “/home” στον HDD δίσκο που μου ξέμεινε από το προηγούμενό μου PC.

συμβουλή: αν έχετε εγκαταστήσει ήδη κάποιο άλλο λειτουργικό εκτός του Linux και αλλάξετε το IDE mode σε RAID mode θα έχετε πρόβλημα το οποίο λύνεται και χωρίς format. Απλά ψάξτε το λίγο.

Ένα καλό site που συμβουλεύτικα για όσα έκανα στο δίσκο είναι αυτό εδώ \[1\] (δείτε τα links πάνω)

Καταρχήν, χρησιμοποιό το ext4 filesystem. Χωρίς swap. Πρέπει να γνωρίζετε ότι όσο περισσότερο γράφουμε στον δίσκο τόσο πιο γρήγορα θα σταματήσει να λειτουργεί στο επιθυμητό επίπεδο. Τόσο πιο γρήγορα θα πρέπει να πάρουμε καινούριο.

Λοιπόν, έφτιαξα ένα partition με το φάκελο root (“/”) στον SSD μου και ένα με το φάκελο “/home” HDD επειδή κατεβάζω και δημιουργώ συνέχεια αρχεία σε αυτόν τον φάκελο!

Έχοντας εγκαταστήσει το Fedora 15, για να δούμε, άραγε ο SSD σας υποστηρίζει το TRIM; (υποθέτως πως είναι ο  /dev/sda) :

> hdparm -I /dev/sda | grep TRIM

(το grep θα ψάξει και θα βρει που βρίσκεται στην έξοδο της εντολής πριν το σύμβολο “|” η λέξη “TRIM”)

Τώρα θα επεξεργαστούμε το αρχείο “/etc/fstab”, είναι ο πίνακας για τα filesystems. Μπορείτε να δημιουργήσετε ένα αντίγραφω, μην πάει κάτι στραβά:

> cp /etc/fstab /etc/fstab.bakup

Πως να το επεξεργαστείτε τώρα; Με το “su -” , δίνοντας τον κωδικό του root (administrator) και έπειτα με “gedit /etc/fstab” θα σας το ανοίξει με τον επεξεργαστή κειμένου. Τώρα, πηγαίνετε στη 2η σελίδα \[4\] του οδηγού, στο βήμα 2 (είναι στα αγγλικά)! Αφορά την υποστήριξη του TRIM command (αν το υποστηρίζει ο δίσκος) ! Πρέπει να το κάνετε! Απλά πρέπει να πάτε στο αρχείο που μόλις ανοιξαμε και να προσθέσετε την παράμετρο “discard” στο partition που εγκαταστήσαμε το root directory (το “/” δηλαδή”)! Πρέπει από **κάπως έτσι**t:

> `/dev/sda1 / ext4 defaults`

Να γίνει  **κάπως έτσι**:

> `/dev/sda1 / ext4 **discard**,defaults`

Αν θέλετε να πειράξετε κάτι άλλο εξαρτάται από εσας, για μέγιστη απόδοση φτάνει και αυτό. Μπορείτε (με ρίσκο για τα δεδομένα σας να προσθέσετε και την παράμετρο “**noatime**“(εγώ την έβαλα καθώς τα δεδομένα που με ενδιαφέρουν βρίσκονται στον HDD μου) Πάντως το συστήνει και ο Linus Torvalds \[5\].

Επόμενο! Έχω  8 GB RAM και δεν φοβάμαι να τα χρησιμοποιήσω όποτε είπα να μεταφέρω τους προσωρινούς φακέλους μου εκεί. Συγκεκριμένα τους “/tmp”, “/var/tmp” and “/var/log”. Πάλι στο “/etc/fstab” πρέπει να προσθέσουμε μερικές γραμμες (το βήμα 6 στον οδηγό). Μία από τις γραμμές που πρέπει να προστειούν στο τέλος του αρχείου είναι πχ. έτσι (για τον φάκελο /tmp):

> `none /tmp tmpfs defaults 0 0`

Το “none” είναι απλά ένα όνομα, θα βοηθήσει μετά για να ξεχωρίζει από τα άλλα.

Μπορούμε επίσης να μεταφέρουμε και την cache του Mozilla Firefox cache σε αυτό το partition (όπως λέει και ο οδηγός)!

Για να δείτε αν δουλεύουν όλα ρολόι εκτελέστε την εντολή “df” και θα σας δείξει τί κάνουν τα partitions σας!

OK, τώρα αν θέλετε και κάτι παραπάνω (με δικόσας ρίσκο πάντα) μπορείτε να απενεργοποιήσετε το journaling του ext4. **Αλλά**! Δεν πρόκειται να πω άλλα καθώς δεν έχω πειράξει άλλο το δίσκο μου. Επιπροσθέτως ήδη προσέθεσα τη παράμετρο “noatime”. Ήδη έχω μεγαλώσει το προσδόκιμο ζωής του δίσκου μου. Μήπως τους κρατάμε και για πολύ;
