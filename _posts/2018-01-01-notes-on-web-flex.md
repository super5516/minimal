---
layout: post
title: "Notes on Web - Flex"
date: 2018-01-01 22:00 +0800
categories:
tags: web css
---

Traditionally, if you want to implement an accordion, you might need javascript. But there's another method that could achieve similar functionality -- the ```flex``` attribute in CSS.

There are plenty of articles detail all the settings and behaviors with ```flex```, like [this one](https://css-tricks.com/snippets/css/a-guide-to-flexbox/). Since ```flex``` is a new attribute that some older browsers could not fully support it, and there are bugs need to be taken care of, you might want to check out the [w3school document about flex](https://www.w3schools.com/cssref/css3_pr_flex.asp) and the [flex bugs and workarounds](https://github.com/philipwalton/flexbugs) before using it.

Recently, I'm playing with a flex box accordion template published on Codepen. The html structure is like

``` html
<div class="flex-container">
  <div class="flex-slide">
    <div class="flex-title"></div>
    <div class="flex-about"></div>
  </div>
</div>
```

And the CSS is like

``` css
.flex-container {
  display: flex;
  overflow: hidden;
  flex-direction: column;
}
.flex-slide {
  flex: 1;
  transition: all 500ms ease;
  overflow: auto;
  overflow-x: hidden;
}
.flex-slide:hover {
  flex-grow: 4;
}
```

And I found that if the contents inside ```flex-slide``` are different, then they won't shrink to the same size when someone gets hovered. After a few trial and errors, I've got a workaround, but I don't know why it works. The workaround is changing the CSS only

``` css
.flex-container {
  width: 955px; /* restrict to desire size */
  display: flex;
  overflow: hidden;
  flex-direction: column;
}
.flex-slide {
  flex: 1;
  min-width: 100px; /* restrict the minimum size after shrinkage */
  max-width: 595px; /* restrict the maximum size after growth */
  transition: all 500ms ease;
  overflow: auto;
  overflow-x: hidden;
}
.flex-slide:hover {
  flex-grow: 4;
  flex-basis: 199px; /* setting the original size of each slide */
}
```

The setting of ```flex-basis``` in ```.flex-slide:hover``` is the one that really affects.
