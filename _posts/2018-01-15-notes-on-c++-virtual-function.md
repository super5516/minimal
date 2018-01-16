---
layout: post
title: "Notes on C++ - Virtual Function"
date: 2018-01-15 1800 +0800
categories:
tags: c++
---

According to the answer of [this question on Stack Overflow](https://stackoverflow.com/questions/2391679/why-do-we-need-virtual-functions-in-c), virtual functions are born to resolve problems when an instance of derived class which is downcasted to its base class. Let's see an example:

``` c++
class Vehicle {
public:
  void describe() { cout << "I can move!" << endl; }
};

class Car : public Vehicle {
public:
  void describe() { cout << "I can move by 4 wheels!" << endl; }
};

int main(void) {
  Vehicle v;
  Car c;
  v.describe(); // I can move!
  c.describe(); // I can move by 4 wheels!

  return 0;
}
```

Both the ```describe()``` functions in ```Vehicle``` and ```Car``` are working as expected. Now we change it a little bit.

``` c++
class Vehicle {
public:
  void describe() { cout << "I can move!" << endl; }
};

class Car : public Vehicle {
public:
  void describe() { cout << "I can move by 4 wheels!" << endl; }
};

void describeVehicle(Vehicle* v) {
  v->describe();
}

int main(void) {
  Vehicle v;
  Car c;
  describeVehicle(&v); // I can move!
  describeVehicle(&c); // I can move!

  return 0;
}
```

To resolve this, we need to add ```virtual``` before ```describe()``` in ```Vehicle```. The result would be like the following example:


``` c++
class Vehicle {
public:
  virtual void describe() { cout << "I can move!" << endl; }
};

class Car : public Vehicle {
public:
  void describe() { cout << "I can move by 4 wheels!" << endl; }
};

void describeVehicle(Vehicle* v) {
  v->describe();
}

int main(void) {
  Vehicle v;
  Car c;
  describeVehicle(&v); // I can move!
  describeVehicle(&c); // I can move by 4 wheels!

  return 0;
}
```

By adding the keyword ```virtual``` before the function in the base class we like to override it, we could invoke the desired function when an object is downcast to its base class.

However, there are times that we think we've override the function but we actually haven't. Maybe we've changed the argument in the base function or we add additional arguments to the derived function.[(ref)](https://stackoverflow.com/questions/39932391/virtual-override-or-both-c)

To prevent this from happening, we could add the keyword ```override``` after the arguments of the derived functions. Using the above example, we could rewrite it as
``` c++
class Car : public Vehicle {
public:
  void describe() override { cout << "I can move by 4 wheels!" << endl; }
}
```

This way, the compiler would check if the derived function ```describe()``` correctly override the base function.

There are situations that the body of the base function is empty. We can use **Pure Virtual Function** provided by C++ like this.
``` c++
class Vehicle {
public:
  virtual void describe() = 0;
}
```

Now we call the base function ```describe()``` as a pure virtual function. And by declaring any single member function in a class as pure virtual function, you would transform that class to an **abstract class**. You cannot create an instance of an abstract class, except by pointer.
``` c++
Vehicle v1; // compile error
Vehicle* v2; // this is ok
```

Furthermore, if the derived class doesn't override the pure virtual function in the base class, it would also become an abstract class.
