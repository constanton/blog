---
title: "Change a Font Awesome icon on hover (using content) + Sopler news!"
pubDate: "2015-02-02T18:11:45.000Z"
description: "Swap Font Awesome icons on hover with CSS, plus a look at Sopler's new task-management features."
---
Hi everyone! The past few days, we made some **major updates** on [Sopler](https://sopler.net "Sopler homepage") that we started designing a long time ago.

It is now possible to set a **due date** or **edit** your items using a brand new options menu. Also, when you enter a **YouTube** link, a (auto-scalable) player will appear on the list! 🙂

Nonetheless, this post concerns changing a Font Awesome icon to another Font Awesome icon when the first one is on hover.

Firstly, I came across this post and a few (unrelated but helpful) answers on Stack Overflow that used the content property. Then, I thought that this might work pretty well and it did.

For example,

```xml
  <div class="divclass">
    <i class="fa fa-circle-o"></i>
  </div>
```

using this CSS:

```css
.divclass{
  font-size:5em;
  color:grey;
  cursor:pointer;
}

.divclass:hover .fa-circle-o:before{
  content:"\f05d";
  color:green;
  opacity:0.4;
}
```

OK, the div element will be a full-width rectangle (use your Developer Toolbar to check what’s going on), but you can modify it later. Anyway, the **result** is: [http://jsbin.com/noqiwi/](http://jsbin.com/noqiwi/ "Example on JS Bin")

It might be trivial but it’s also a lot easier than other implementations I’ve seen so far.
