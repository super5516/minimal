---
layout: post
title: "Notes on C++ - static variable and static function"
date: 2017-12-26 20:00 +0800
categories:
---

Static variable is a variable that cannot be changed after initialization.

Example:
``` c++
static int s_i = 10;
s_i = 20; // this would cause a compile error
```

Static variable in a class has the same characteristic as the normal static variable, plus that it's shared by all the instances of that class.

Example:
``` c++
Class Book {
private:
  static int counter;
  int id;
public:
  Book() {this->id = counter++;};
};

int Book::counter = 0; // need to initialize first

int main (void) {
  Book b1; // b1.id = 0
  Book b2; // b2.id = 1
}
```

Static function in a class is a function that could be called without any instance.

Example:
``` c++
Class Book {
private:
  static int counter;
public:
  static int getCounter();
};

int Book::counter = 0;

int main (void) {
  Book::getCounter(); // it's ok
}
```

_Questions unsolved_
- What's the meaning of a normal static function? If it has the exact functionality of a normal function, could we omit it?
