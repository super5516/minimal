---
layout: post
title: "Notes on OpenGL - VAO and VBO"
date: 2018-02-14 1100 +0800
categories:
tags: opengl
---

VBO is used for storing data such as the coordinates of the object you want to draw, the setting of a color, or the order of a set of coordinates that you want the OpenGL core function to draw in.

VAO is used for storing buffers that tell the OpenGL core function some rules to follow.

However, even though a VAO could store multiple VBOs, it could only contain one object to draw.

_Note: This post is based on my knowledge about OpenGL. Since I'm a newbie, there might be some error in this post._
