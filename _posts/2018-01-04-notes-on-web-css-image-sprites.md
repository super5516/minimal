---
layout: post
title: "Notes on Web - CSS Image Sprites"
date: 2018-01-04 22:00 +0800
categories:
tags: web
---

Tien-Yu just asked and explained to me what is **CSS Image Sprites**. Just making some rough notes.

Typically, if you want to insert images or icons, you would used something like ```background-image``` in css, or include an icon package like font-awesome. When there are a lot of images or icons on your webpage, it might take a while to fully load them, even after you shrink them in size. Using **CSS Image Sprites** may speed up the loading process.

**CSS Image Sprites** is a technique that combine images or icons into one bigger image, and only display the desired portion of it at desired place. Thinking about that, if you have 30 images or icons combined to 1 image, you would only need 1 HTTP request to get all of them. You could reduce the amount of HTTP request as well as the amount of time transferring data.

In fact, there is another way of inserting image -- creating SVG image by code. The pros are that you could easily modify your image, and that you don't even need a HTTP request to get your image, while the cons are that you might get a huge size of web file, and that the browser would take some efforts to transform codes into images. _I haven't do some research on creating SVG image by code so there might be some error in it._
