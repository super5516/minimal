---
layout: post
title: "Notes on C++ - Takeaway from Singleton Pattern"
date: 2018-03-02 2030 +0800
categories:
tags: c++
---

The purpose of Singleton Pattern is that you want to have a single instance of an object through out the entire program (ex. a database).

To achieve this, we'll need the keyword ```static``` to help us create the instance.

``` c++
class SingletonObject {
private:
  SingletonObject() {}
public:
  static SingletonObject& get() {
    static SingletonObject so;
    return so;
  }
  
  void do_something() {}
  
  SingletonObject(const SingletonObject&) = delete;

  SingletonObject& operator=(const SingletonObject&) = delete;
};

int main(void) {
  SingletonObject::get().do_something();
  return 0;
}
```

Some key points to make an object a Singleton:
- declare the constructor as private so that no one could create an instance except itself.
- delete the copy constructor and overload the assignment operator so that nothing could duplicate the instance.
- define a static function to declare and return a static instance so that every time you invoke the function, you would get the exact instance.
