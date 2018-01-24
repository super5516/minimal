---
layout: post
title: "Notes on C++ - Takeaway from Builder Pattern"
date: 2018-01-24 2200 +0800
categories:
tags: c++
---

Recently, I've been taking an online course about the design pattern, and the Builder Pattern is the first pattern I learned. Here are some takeaways I've got.

The purpose of Builder Pattern is to make it easier to construct a complicated object. Let's say we have a class like the following.
``` c++
class Person {
private:
  string first_name, last_name;
  string address, email_address;
  int income, age;
};
```

Usually, we'll make some Setter and Getter to set and get those member variables. Therefore, to completely construct an instance of ```Person```, we'll need to call the setters for each member variable. In this example, we would need to call a total of 6 setter, and it's just for this slightly complicated object. If there are much more member variables, or even some other classes inside, that's horrible.

And here comes the Builder, which could take care of the creation process. So we would write a Builder like the following.
``` c++
class PersonBuilder {
private:
  Person p;
public:
  PersonBuilder() {
    p = Person(); // initialize an instance of person
  }
  PersonBuilder& named(const string& first_name, const string& last_name) {
    p.setFirstName(first_name); // remember to make the setters
    p.setLastName(last_name);
    return *this;
  }
  PersonBuilder& livesAt(const string& address) {
    p.setAddress(address);
    return *this;
  }
  PersonBuilder& withEmail(const string& email_address) {
    p.setEmailAddress(email_address);
    return *this;
  }
  PersonBuilder& ages(int age) {
    p.setAge(age);
    return *this;
  }
  PerosnBuilder& withIncome(int income) {
    p.setIncome(income);
    return *this;
  }
};
```

With ```PersonBuilder``` we could now construct an instance of ```Person``` using the member functions. Now you might be wondering why we need this builder? We still have to invoke lots of member functions to completely construct an instance of ```Person```. You're right, thus we need to add some final touches to make it truely useful.
``` c++
class Person {
private:
  ...
public:
  ...
  static PersonBuilder create() { return PersonBuilder(); }
};

class PersonBuilder {
private:
  ...
public:
  ...
  Person build() { return p; }
};
```

Now, we could build a ```Person``` like the following.
``` c++
int main(void) {
  Person p = Person::create().named("Peng-Yi", "Chou").livesAt("Taiwan").withEmail("abc@gmail.com").ages(24).withIncome(10000).build();

  return 0;
}
```

So, what's good about using a builder? To me, not conly could I build a complicated object in one line, but I could give the setters another name, so that if someone else uses my code in the future, he or she could easily understand what each function is going to set.

Note that to make a builder building an object in one line is due to the return type of the member functions. They return a reference to the object itself, so that we could continue invoking other member functions without a semicolon.
