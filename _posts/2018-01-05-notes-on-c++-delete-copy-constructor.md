---
layout: post
title: "Notes on C++ - Delete Copy Constructor"
date: 2018-01-05 21:00 +0800
categories:
tags: c++
---

Assume you have the following code

``` c++
class Foo {
  // something here
};

int main (void) {
  Foo foo1;
  Foo foo2;
}
```

If you want to disable the copy constructor for a class, which means you don't want something like ```foo2 = foo1;``` or ```Foo foo3 = foo1;``` happen, you could delete the copy constructor like the following code

``` c++
class Foo {
public:
  Foo(const Foo&) = delete; // disable Foo foo3 = foo1;
  Foo& operator=(const Foo&) = delete; // disable foo2 = foo1;
};
```

Then ```foo2 = foo1;``` or ```Foo foo3 = foo1;``` would result in compile error.

Also note that if you delete the copy constructor of the base class, you also delete all the copy constructo of the derived class. The same thing won't happen in the contrary.

Example:
``` c++
class BaseFoo {
public:
  BaseFoo(const BaseFoo&) = delete;
  BaseFoo& operator=(const BaseFoo&) = delete;
};

class DerivedFoo : public BaseFoo {
 // something here
};

int main (void) {
  BaseFoo b_foo1;
  BaseFoo b_foo2;
  BaseFoo b_foo3 = foo1; // compile error
  b_foo2 = b_foo1; // compile error

  DerivedFoo d_foo1;
  DerivedFoo d_foo2;
  DerivedFoo d_foo3 = d_foo1; // also compile error
  d_foo2 = d_foo1; // also compile error
}
```
