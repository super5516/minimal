---
layout: post
title: "Notes on Web - Spaces Between Inline-Blocks"
date: 2018-03-21 2000 +0800
categories:
tags: web css
---

Recently I've been trying to create 2 elements within a row that sit side by side, so I wrote something like this:

html:
``` html
<div class="container">
  <div class="element1"></div>
  <div class="element2"></div>
</div>
```
css:
``` css
.element1, .element2 {
  display: inline-block;
  width: 50%;
}
```

And then something weird happened, how come ```element2``` is placed under ```element1```? Both ```element1``` and ```element2``` are of 50% width, and should be displayed in a single line, why did they behave like they are too wide to fit in a single row?

According to [this post](https://stackoverflow.com/questions/6871996/two-inline-block-width-50-elements-wrap-to-second-line), it's due to the white space that are automatically created between ```inline-block```s.

There are many workarounds in that post. For me, I choose this one:
``` css
.container {
  white-space: nowrap;
}
```

Which seems rational for me and keeps the readability of the code.
