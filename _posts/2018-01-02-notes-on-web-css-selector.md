---
layout: post
title: "Notes on Web - CSS Selector"
date: 2018-01-02 22:00 +0800
categories:
tags: web css
---

Found a simplified way of writing CSS file. If you got a CSS file like this

``` css
.home {
 
}
.home-btn {

}
.home-title {

}
.home-btn:hover {

}
```

Then you could rewrite as

``` css
.home {
  &-btn { /* equals to .home-btn */
    &:hover { /* equals to .home-btn:hover  */

    }
  }
  &-title { /* equals to .home-title */

  }
}
```

The ```&``` sign just replace the selector keyword so this will work the same as the original one.
