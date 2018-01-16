---
layout: post
title: "Notes on C++ - Enum"
date: 2018-01-16 1800 +0800
categories:
tags: c++
---

There are many discussions on the Internet trying to figure out why we need ```enum``` in C++ [(ref1)](http://www.cplusplus.com/forum/beginner/12821/)[(ref2)](https://stackoverflow.com/questions/899917/why-do-people-use-enums-in-c-as-constants-while-they-can-use-const).

I think the following reasons are sufficient to persuade me of using it in my code:
- Give names, which could contain their meaning, to a set of related variables so that others could easily grasp the idea of your code.
- It could be treated as type, or class.

Let's see an example:
``` c++
enum { STAGE_1, STAGE_2, STAGE_3 };

int main(void) {
  int flag;
  if (/* some condition */) flag = STAGE_1;
  else if (/* some other condition */) flag = STAGE_2;
  else flag = STAGE_3;

  return 0;
}
```

As we could see, by using ```enum```, we could know that ```flag``` would change to different stages according to different conditions. Indeed this could also be done by using ```#define``` or ```const int```, so let's change it a little bit:
``` c++
enum Stage { STAGE_1, STAGE_2, STAGE_3 };

Stage getStage() {
  if (/* some condition */) return STAGE_1;
  else if (/* some other condition */) return STAGE_2;
  else return STAGE_3;
}

int main(void) {
  Stage st = getStage();
}
```

The keywork ```enum``` has change it to a type, you could declare a variable and send it to or receive it from a function.

However, this isn't a good code. It could potentially generate bugs that are hard to find. First, we need to understand how C++ compiler deals with ```enum```.

If you print out the value of, for example, ```STAGE_1```, you would find that it's actually an integer of the value 0. C++ compiler would by default change the variables in a enum to integers imcrement from 0. So the example is actually like this.
``` c++
enum Stage {
  STAGE_1 = 0,
  STAGE_2 = 1,
  STAGE_3 = 2
}
```

We could set the value manually just by setting the desired value to the variable.
``` c++
enum Stage {
  STAGE_1, // still 0
  STAGE_2 = 5,
  STAGE_3 // changed to 6
}
```

After knowing this, we could find out that an ```enum``` variable is capable of casting to an ```int```. And this could potentially generate bugs [(ref)](https://stackoverflow.com/questions/18335861/why-is-enum-class-preferred-over-plain-enum).

To prevent this, we could add the keyword ```class``` after ```enum```. By doing so, that ```enum``` could no longer cast to an ```int```.
``` c++
enum class Stage { STAGE_1, STAGE_2, STAGE_3 };

Stage getStage() {
  if (/* some condition */) return Stage::STAGE_1; // cannot refer to it simply by STAGE_1
  else if (/* some other condition */) return Stage::STAGE_2;
  else return Stage::STAGE_3;
}

int main(void) {
  int i = getStage(); // compile error
  Stage st = getStage();

  return 0;
}
```


