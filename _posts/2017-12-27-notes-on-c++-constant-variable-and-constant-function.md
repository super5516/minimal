---
layout: post
title: "Notes on C++ - Constant Variable and Constant Function"
date: 2017-12-27 22:00 +0800
categories:
---

[(ref1)](https://scriptjerks.blogspot.tw/2012/07/cconst.html)
[(ref2)](http://blog.xuite.net/tsai.oktomy/program/65131235-const+%E6%94%BE%E7%BD%AE%E4%BD%8D%E7%BD%AE%E7%9A%84%E6%84%8F%E7%BE%A9)

Constant variable has the characteristic that once it's initialized, its value cannot be changed.

Example:
``` c++
const int c_i = 10;
c_i = 20; // compile error
```

Also, you need to assign value on initialization, or you'll get a compile error.

Example:
``` c++
const int c_i; // compile error
c_i = 20;
```

Now we know what is a normal constant variable. How about a constant pointer variable? It would depends on how you placed the keyword `const`.

Example:
``` c++
const int* ci_ptr1; // the value pointed by ci_ptr1 cannot be changed
int const* ci_ptr2; // same as ci_ptr1
int* const ci_ptr3; // the memory address pointed by ci_ptr3 cannot be changed
const int* const ci_ptr4; // both the value and the memory address pointed by ci_ptr4 cannot be changed
```

