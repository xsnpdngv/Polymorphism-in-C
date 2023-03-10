% Polymorphism in C  
% Tamás Dezső  
% February 3, 2023

A way to achieve polymorphism in C
==================================


Introduction
------------

This poroject demonstrates through a simple example how polymorphism
can be achieved in C.


Polymorphism
------------

Polymorphism is key to Object Orientation. It means that seemingly the
same thing can behave differently, depending on the actual underlying
type.

```c++
obj.func()
```

The behavior of `func` depends on the type of `obj`, therefore `func` is
polymorphic.

Saying _"Polymorphism can be achieved by using switch statements
or long if/else chains within a function."_ would be true without
the following addition:

>  The mechanism of polymorphism must not create a source code
   dependency from the caller to the callee.

We desire systems built with dynamic polymorphism because they are
strongly decoupled. Dependencies can be inverted across architectural
boundaries. They are testable using Mocks and Fakes and other kinds of
Test Doubles. Modules can be modified without forcing changes to other
modules. This makes such systems much easier to change and improve.


Goal
----

To have something like this in C

```c++
Developer *developer = new SeniorDeveloper();
developer->WriteCode("hello world");
delete developer;
```

..for example in the following way:

```c
developer_t *developer = (developer_t *)seniorDeveloper_Create();
developer_WriteCode(developer, "hello world"); /* needs passing the object */
developer_Destroy(developer);
```

Hence the aim is to make possible to

- extend _Data Structure_ and
- alter _Behaviour_

of a type/class/struct.


SOLID Aspects
-------------

SOLID gives 5 software design principles to build understandable,
flexible and maintainable (Object Oriented) code. In this mnemonic O
is for Open/Closed Principle, L is for Liskov Substitution Principle.
Both are strongly related to polymorphism.


### O: Open/Closed Principle

Software entities (classes, modules, functions, etc.) should be open for
extension, but closed for modification.

A class is closed, since it may be compiled, stored in a library,
baselined, and used by client classes. But it is also open, since any
new class may use it as parent, adding new features. When a descendant
class is defined, there is no need to change the original or to disturb
its clients.


### L: Liskov Substitution Principle (LSP)

The Liskov Substitution Principle (LSP) states that objects of a
superclass should be replaceable with objects of its subclasses without
breaking the application.

In other words, what we want is to have the objects of our subclasses
behaving the same way as the objects of our superclass.

Rubberduck example explains what LSP suggests to avoid.



Run
---

```bash
mkdir build
cd build
cmake ..
make
./poly_main

# 2>/dev/null to print only WriteCode()'s output
# >/dev/null to print only function callings
```
