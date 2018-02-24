---
layout: post
title: "Using Boost in Clion"
date: 2018-02-15 2000 +0800
categories:
tags: c++ clion boost
---

Recently, I want to try some useful and powerful functions in [Boost](http://www.boost.org/) on Clion.

However, the [official documentation](https://www.jetbrains.com/help/clion/quick-cmake-tutorial.html#d99293e295) about how to set up boost doesn't work for me.

So I searched through lots of the similar questions and finally found [one solution](https://stackoverflow.com/questions/36211915/trying-to-add-boost-libraries-to-cmake-txt-clion-ide) that works for me.

Seems that if you put the Boost library in some folder that doesn't match the default path of what Clion assumed, it cannot found the library. Maybe that's why you need to set up many variables before ```find_package()```.
