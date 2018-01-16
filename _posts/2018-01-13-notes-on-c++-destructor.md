---
layout: post
title: "Notes on C++ - Destructor"
date: 2018-01-13 2000 +0800
categories:
tags: c++
---

Assuming we have the following code:

``` c++
class Shape {
public:
  Shape() {}
}

int main(void) {
  Shape s;

  return 0;
}
```

Just before the program terminates, the instance of class ```Shape``` will invoke a destructor, which was automatically created by the compiler, and delete itself.

However, we could define the destructor ourselves like this:
``` c++
class Shape {
public:
  Shape() {}
  ~Shape() {} // this is the destructor
}
```

Like the constructor, we could write something in the body of the destructor. For example, we could output some message so that we know the destructor is invoked.

When we're creating a class pointer rather than an instance, we need to remember to free the memory space pointed by the pointer.
``` c++
class Shape {
public:
  Shape() {}
  ~Shape() {}
}

int main(void) {
  Shape* s = new Shape();

  delete s; // remember to free the memory

  return 0;
}
```

Things would get more complicated if we have some inheritance in our code. let's see this example.
``` c++
class Shape {
public:
  Shape() { cout << "Shape constructor." << endl; }
  ~Shape() { cout << "Shape destructor." << endl; }
}

class Square : public Shape {
public:
  Square() { cout << "Square constructor." << endl; }
  ~Square() { cout << "Square destructor." << endl; }
}

int main(void) {
  Square sq;

  return 0;
}
```

The output would be
``` sh
Shape constructor.
Square constructor.
Square destructor.
Shape destructor.
```

But if we change it a little bit.

``` c++
int main(void) {
  Shape* sq = new Square();

  delete sq;

  return 0;
}
```

The output would be
``` sh
Shape constructor.
Square constructor.
Shape destructor.
```

The Square destructor hadn't been invoked. To make sure we free all the memories we allocated, we need to change the destructor in the base class to **Virtual Destructor**.
``` c++
class Shape {
public:
  Shape() { cout << "Shape constructor." << endl; }
  virtual ~Shape() { cout << "Shape destructor." << endl; }
}
```

Then we will get the desired output, and we are sure that all the memories we allocated were freed.
