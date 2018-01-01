---
layout: post
title: "Notes on Web - vh and vw"
date: 2017-12-29 20:00 +0800
categories:
tags: web css
---

When it comes to setting height or width of a HTML element, you might use something like

``` css
.sample {
height: 100px;
width: 85%;
}
```

If your element do not change according to different screen sizes, then a fixed number (```px```) or a portion of its parent element (```%```) might be sufficient. But if your element do, them a portion of the screen size might be very useful.


```vh``` and ```vw``` are attributes that are used to set the height and width as a portion of the screen size while the page was loaded. (which means you need to refresh your webpage to see the effect if you change the size of your browser)

``` css
.sample {
height: 90vh; /* set the height to 90% of the screen height */
width: 50vw; /* set the width to 50% of the screen width */
}
```
