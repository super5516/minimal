---
layout: post
title: "Notes on C++ - Constructor"
date: 2018-01-06 2000 +0800
categories:
tags: c++
---

There are some way of writing a constructor, depends on your need.

1. Basic One

    ``` c++
    class Point {
    public:
      Point();
    }

    int main (void) {
      Point p; // an instance of class Point is created
    }
    ```

    This is the basic constructor, which would create an instance when declared.

2. With Declaration

    One can do something during the construction, either an one-line function or a full declaration function is ok.

    ``` c++
    class Point {
    public:
      // this is an one-line function
      Point() { cout << "I'm the constructor" << endl; };
    }

    int main (void) {
      Point p;
    }
    ```

    ``` c++
    class Point {
    public:
      Point();
    }

    // this is a full declaration function
    Point::Point() {
      cout << "I'm the constructor" << endl;
    }

    int main (void) {
      Point p;
    }
    ```

    Both the above two examples will print out "I'm the constructor" in the console. For simplicity, the following examples will use the full declaration function.

3. With Arguments

    By passing arguments into the constructor, we can do much more things while creating an object.

    ``` c++
    class Point {
    private:
      int x;
    public:
      Point(int val);
    }

    Point::Point(int val) {
      x = val;
    }

    int main (void) {
      Point p(5); // now the x of object p would be set to 5
    }
    ```

    Actually, you can use the ```this``` pointer to make your code more like your intuition.

	``` c++
	class Point {
	private:
	  int x;
	public:
	  Point(int x);
	}

	Point::Point(int x) {
	  this->x = x;
	}
	```

	```this->x``` refers to the member variable inside the Point object. You could also omit the argument name in class declaration.

	``` c++
	class Point {
	private:
	  int x;
	public:
	  Point(int);
	}
	```
4. With Initialization

	You could furthur simplify the assignments if they are as straight forward as something like ```x = val;``` in the above example.

	``` c++
	class Point {
	private:
	  int x;
	  int y; // we use two member variables to demonstrate this
	public:
	  Point(int val1, int val2) : x(val1), y(val2);
	  // the above line equals to the following 2 lines
	  // x = val1;
	  // y = val2;
	}
	```

	Of course you could write it like this

	``` c++
	class Point {
	private:
	  int x;
	  int y;
	public:
	  Point(int, int);
	}

	Point::Point (int x, int y) : x(x), y(y) {
	  // do something
	}
	```
