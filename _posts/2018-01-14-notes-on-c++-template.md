---
layout: post
title: "Notes on C++ - Template"
date: 2018-01-14 2000 +0800
categories:
tags: c++
---

When we want to create a function that simply add two ```int```, we could write the following codes.

``` c++
int add(int a, int b) {
  return a + b;
}

int main(void) {
  int a = 10;
  int b = 5;

  cout << add(a, b) << endl; // 15
}
```

Now that we might need to expand the functionality of ```add()```, let's say we want to make it capable of adding two ```double```. By the overload nature of C++, we could achieve this like this.

``` c++
int add(int a, int b) {
  return a + b;
}

double add (double a, double b) {
  return a + b;
}

int main(void) {
  double a = 10.1;
  double b = 5.5;

  cout << add(a, b) << endl; // 15.6
}
```

If we need to further expand the functionality, we would need to add huge chunk of similar codes, with only the differences in types. To avoid this tedious writing, we could use ```template``` as follows.

``` c++
template<typename T> T add(T a, T b) {
  return a + b;
}

int main(void) {
  cout << add(10, 5) << endl; // 15
  cout << add(10.1, 5.5) << endl; // 15.6

  return 0;
}
```

The compiler would automatically change the type ```T``` to the type of the variable the function takes in. Now we only need one function to perform the addition of ```int``` and ```double```. Actually, it could perform the addition of two variables with the same type (the type would need to support ```+``` operator or will get a compile error on ```return a + b;```). Note that the keyword ```typename``` is **in most case** interchageable with the keyword ```class```.
