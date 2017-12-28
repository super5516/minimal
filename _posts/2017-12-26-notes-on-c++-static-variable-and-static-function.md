---
layout: post
title: "Notes on C++ - static variable and static function"
date: 2017-12-26 20:00 +0800
categories:
tags: c++
---

Static variable is a variable like global variable, except that it can only be accessed within the proper scope.

Example:
``` c++
void incCounter() {
  static int counter = 0;
  counter++;
}

int main (void) {
  incCounter(); // counter = 1
  incCounter(); // counter = 2
  counter++; // compile error
}
```

Static member variable (static variable in a class) has the same characteristic as the normal static variable, plus that it's shared by all the instances of that class.

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

Static member function (static function in a class) is a function that could be called without any instance. Note that static member function could only access static member variables, which means it cannot access normal member variable, nor can it access normal member function. [(ref)](http://kamory0931.pixnet.net/blog/post/119201381)

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
