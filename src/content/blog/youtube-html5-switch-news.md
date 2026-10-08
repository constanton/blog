---
title: "YouTube HTML5 Switch (and other news)"
pubDate: "2012-12-03T15:38:14.000Z"
description: "Introducing a Firefox add-on that switches YouTube to HTML5 playback to avoid unreliable Flash."
---
Hello! Long time no see!

It’s been a busy period and I have lots of news to share. First of all, I decided to have a look on the Mozilla [Add-on SDK](https://addons.mozilla.org/en-us/developers/builder "Mozilla Add-on SDK") . It has a very simple API to create Add-ons for Firefox.

Anyway, I tried to come up with an idea of what would be my first Add-on. Hmmm…An Add-on that can make my web experience less annoying. Considering that I spend half of my time on YouTube to listen to songs (mostly), view videos etc, as a Linux user, I get really annoyed when the Flash plug-in crashes and I have to restart Firefox.  You can always visit [youtube.com/html5](https://www.youtube.com/html5 "html5 page") to change that but what if you delete your cookies? It’s a boring procedure.

![youtube\_html5\_switch\_logo](../../assets/images/2012/12/html5switch100.jpeg)

YouTube HTML5 Switch logo

So, what I thought was to make an Add-on that would simply add the “html5=1” parameter on the URL. And I did it…well, kind of, it’s now an experimental Add-on for Firefox. I need to add some more features for it to be considered as a proper Add-on. It’s called “YouTube HTML5 Switch” and [here it is](https://addons.mozilla.org/addon/youtube-html5-switch?src=external-blog "YouTube HTML5 Switch") at the Mozilla Add-ons website, and [here is](https://github.com/constanton/youtube_html5_switch "YouTube HTML5 Switch on Github") the source code on Github.

I currently develop the Add-on at the [Add-on Builder](https://builder.addons.mozilla.org/) (that means online). I will eventually download the SDK and try it on Fedora 🙂 It’s not the smartest Add-on in the world, but I think it’s a good start for a newbie. By the way I need to say that the SDK’s documentation is not very helpful and I needed to google **a lot** to write down a few lines of code. Anyway, in every “major” release I will be posting here any changes etc. You can also read the README.md on Github.

What’s more? [Wonky Doll and the Echo](http://wonkydollandtheecho.com/ "Wonky Doll and the Echo website") (the band where I play) are supporting [I Like Trains](https://en.wikipedia.org/wiki/I_Like_Trains "I Like Trains Wikipedia") here in Athens on December 15, 2012. You can check our [Bandcamp](http://wonkydollandtheecho.bandcamp.com "Wonky Doll and the Echo Bandcamp") page and listen to our songs. Now, if you have installed the Add-on you can test it with these video…if you go on YouTube of course 🙂

Some videos like this for instance don’t have an HTML5 player so the plugin will not be of any use here.  

<iframe src="https://www.youtube.com/embed/pyWYgLhChyw?version=3&amp;rel=1&amp;showsearch=0&amp;showinfo=1&amp;iv_load_policy=1&amp;fs=1&amp;hl=en&amp;autohide=2&amp;wmode=transparent" title="Embedded video" loading="lazy" allow="fullscreen; picture-in-picture; encrypted-media" allowfullscreen></iframe>

Other videos though, do have have an HTML5 version and the plugin will work!

<iframe src="https://www.youtube.com/embed/99AN768ekuU?version=3&amp;rel=1&amp;showsearch=0&amp;showinfo=1&amp;iv_load_policy=1&amp;fs=1&amp;hl=en&amp;autohide=2&amp;wmode=transparent" title="Embedded video" loading="lazy" allow="fullscreen; picture-in-picture; encrypted-media" allowfullscreen></iframe>
