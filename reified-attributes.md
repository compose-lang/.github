# Reified attributes

The [deadly diamond of death](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem) problem has 2 legs: methods and attributes.

**Deadly diamond of methods**

In a genuine diamond inheritance tree, such as allowed for classes by Python and C++ and for interfaces in Java or C#, there are ways to address collision of methods: MRO (Method Resolution Order) in Python, override and redirect in C++, Java and C#. One might think that they are not _elegant_, but they work. Syntactic sugar might be a nice to have, but that's not worth a new programming language...

**Deadly diamond of attributes**

However, no existing language except [prompto](https://prompto.org/reference) safely supports multiple inheritance of attributes. C++ duplicates attributes, which is disastrous (which attribute does ```this->name``` refer to?). Java and C# avoid the problem altogether by only allowing a single class inheritance tree, and forbidding attributes in interfaces. Similarly Scala forbids attributes in traits. Python lets anything happen i.e. an attribute can be treated as an int in class A and as a str in class B, leading to disasters in a class C that inherits from A and B...

Much like prompto, Compose solves this problem by introducing reified attributes.

In Compose an attribute can be declared _outside_ any class, as follows:

```
attribute brand: string | null;
```

It can later be used when declaring a class:

```
class Device(brand) {}
```

Let's consider the following inheritance scenario:

```
attribute brand: string | null;
attribute voltage: float;
class Device(brand) {}
class Phone(voltage) extends Device {}
class Computer(voltage) extends Device {}
class SmartPhone extends Phone, Computer {}
```

The attribute `brand` is carried _once_ and _once only_ across the inheritance tree. In C++, there would be 2 `brand` attributes. In Python there would be only 1 and it would be consistent (coming from 1 definition).
The attribute `voltage` is also _once_ and _once only_ across the inheritance tree. In C++, there would be 2 `voltage` attributes. In Python there would be only 1 but it would be inconsistent (could be an int in Phone, and a string in Computer).
With Compose, there is only 1 consistent `voltage` attrinute.

This makes it possible to infinitely compose classes from existing ones without fearing inconsistencies.

A quick note re wording: when using inheritance, it is common to say that `Phone` _is a_ `Device`. When using composition, developers prefer saying that a `SmartPhone`_has a_ `Phone` and _has a_ `Computer`. Compose lets you say that a `SmartPhone`_is a_ `Phone` and _is a_ `Computer`. It is both _composed of both_, and _one of each_.   






