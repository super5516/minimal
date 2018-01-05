---
layout: post
title: "Git Config File Location"
date: 2018-01-03 20:00 +0800
categories:
tags: git wls
---

According to [this article](http://www.linux-pages.com/2016/09/where-is-git-config-file/), the Git configuration file ```.gitconfig``` may be located in the following places:
- ```.git/config``` in the repository folder
- ```~/.gitconfig```

Since I'm using Windows 10 Linux Subsystem, I do find the configuration file in these two location. The difference between these two is that the former would only affect the repository it resides in, while the latter is like global setting.
