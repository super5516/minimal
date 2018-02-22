---
layout: post
title: "Notes on C++ - Something About Vector"
date: 2018-02-22 2230 +0800
categories:
tags: c++
---

```vector``` is a convinient container in C++ Standard Template Library(STL). It acts like a queue, which means you can only insert element from the back and delete element from the front(there is actually a member function that could delete element at any position, but it would take you more than O(1) time).

You don't need to specify the size when initialize, it would grow or shrink when you insert or delete elements.

Furthermore, you could access elements inside the vector like an ordinary array, like ```my_vector[5]```.

To provide such convinience, a ```vector``` would try to find a continuous memory location to store all the elements. And it would relocate when the size is changed.

So here comes a potential bug you might face sometimes. Think about the following code.

``` c++
int main(void) {
  vector<int> my_vector;
  for(int i = 0; i < 10; i++)
    my_vector.push_back(i);
  int& fifth_element = my_vector[4];
  my_vector.push_back(11);
  cout << fifth_element << endl; // what is the printed value?
}
```

It's not 4.

Recall that a ```vector``` would relocate if the size is changed, so the memory space we were referencing is now occupied by something we don't know. Note that the same thing would happen if you use a pointer.

So remember, if the size of your ```vector``` would change in the future, DO NOT use variables that refers to or points to any element inside.
