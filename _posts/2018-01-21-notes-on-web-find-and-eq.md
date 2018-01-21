---
layout: post
title: "Notes on Web - find() and eq()"
date: 2018-01-21 2100 +0800
categories:
tags: web jquery
---

```find()``` is a useful function in jQuery. According to the [jQuery API Documentation](http://api.jquery.com/), ```find()``` is similar to ```childern()```, and the only difference is that the latter only travels a single level down the DOM tree.

You could put selector or element in the parenthesis, and the function will return all the elements that match.

Html:
``` html
<div>
  <ul>
    <li>first</li>
    <li>second</li>
    <li>third</li>
  </ul>
</div>
```
Javascript:
``` js
$("div").find("li"); /* first, second, third would be returned */
$("div").children("li"); /* nothing would be returned */
```

By using ```eq()```, you can choose the desired element within a group. Inserting the index of the desired element (starts from 0) or add a negative sign to select from the end (starts from 1).

Continue from the above example:
``` js
$("div").find("li").eq(0); /* first would be returned */
$("div").find("li").eq(-1); /* third would be returned */
```
