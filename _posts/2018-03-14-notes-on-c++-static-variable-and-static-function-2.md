---
layout: post
title: "Notes on C++ - Static Variable and Static Function 2"
date: 2018-03-14 2200 +0800
categories:
tags: c++
---

In a previous [post](https://super5516.github.io/2017/12/26/notes-on-c++-static-variable-and-static-function.html) I've mentioned an unresolved question about the normal static function. And here are some explanation.

The keyword ```static``` in C++ is used to describe the lifetime of a variable or a function. If you declare a variable/function outside any blocks, then the variable/function could only be accessed/invoked inside the file where it's written.

``` c++
// file_a.cpp
static int s_i = 0;
static void print() { cout << "Hi!" << endl; }

void func_a() {
  s_i = 10;
  print();
}

// file_b.cpp
void func_b() {
  s_i = 20; // compile error
  print(); // compile error
}
```
