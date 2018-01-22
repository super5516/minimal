---
layout: post
title: "Notes on C++ - Customize Printing Function with Ostream"
date: 2018-01-22 23:00 +0800
categories:
tags: c++
---

We know that ```std::cout``` is a very powerful function that could print almost everything onto the console, but when you got some complex objects and there are lots of different fields to display, a customized printing function would be better.

``` c++
class Person {
private:
  string first_name, last_name;
public:
  Person(string first_name, string last_name) : first_name(first_name), last_name(last_name) {}
  ~Person() {}
  friend ostream& operator<<(ostream& os, const Person& obj) {
    os << "This person is named " << obj.first_name << " " << obj.last_name;
  }
};

int main(void) {
  Person p1("Peng-Yi", "Chou");
  cout << p1 << endl; // This person is named Peng-Yi Chou

  return 0;
}
```

What we did is that we override the operator ```<<``` for class ```Person```, so that when we send the instance of it to ```std::cout```, we could print out the desired contents without lots of coding.

Note that since we declared the member variable ```first_name``` and ```last_name``` as ```private```, we need to make the customized printing function a friend to the class (just add the keyword ```friend``` in front of the function). And now we could directly access those variables inside the function.

An alternative way is to define some getter function to get the member variable.
