# Object-Oriented Programming (OOP) Cheat Sheet

As the name suggests, Object-Oriented Programming or Java OOPs concept refers to languages that use objects in programming, they use objects as a primary source to implement what is to happen in the code. Objects are seen by the viewer or user, performing tasks you assign.

Object-oriented programming aims to implement real-world entities like inheritance, hiding, polymorphism, etc. in programming. The main aim of OOPs is to bind together the data and the functions that operate on them so that no other part of the code can access this data except that function.

## Pillars

### I. Encapsulation

_Hides an object's internal state and functionality, only allowing access through a public set of functions._

- Encapsulation can be achieved by declaring all the variables in a class as private and writing public methods in the class to set and get the values of the variables.
  - Usually with public `getter` and `setter` methods within the class.
- The variables or the data in a class is hidden from any other class and can be accessed only through any member function of the class in which they are declared.
- Data in a class is hidden from other classes, which is similar to what data-hiding does; therefore, the terms “_encapsulation_” and “_data-hiding_” are used interchangeably.

### II. Abstraction

_Hides unnecessary implementation code, only revealing internal mechanisms that are relevant for other objects._

- In Java, abstraction is achieved by interfaces and abstract classes. We can achieve 100% abstraction using interfaces.
- The abstract method contains only method declaration, but not implementation.

### III. Inheritance

_Allows classes to reuse code and properties from other classes._

- It is the mechanism in Java by which one class is allowed to inherit the features (fields and methods) of another class.
- We are achieving inheritance by using `extends` keyword.
- Inheritance is also known as “_is-a_” relationship.

**Superclass**

- The class whose features are inherited is known as superclass (also known as base or **parent class**).

**Subclass**

- The class that inherits the other class is known as subclass (also known as **derived class** or **extended class** or **child class**). - The subclass can add its own fields and methods in addition to the superclass fields and methods.

**Reusability**

- Inheritance supports the concept of “_reusability_”, i.e. when we want to create a new class and there is already a class that includes some of the code that we want, we can derive our new class from the existing class. By doing this, we are reusing the fields and methods of the existing class.

### IV. Polymorphism

_Allows objects to take on more than one form and share behaviors._

**Overloading (Compile-Time Polymorphism, Static Polymorphism, or Early Binding)**

- In Java, a method signature is composed of a name and the number, type, and order of its parameters.
- Changing the Number of Parameters.
- Changing Data Types of the Arguments.
- Changing the Order of the Parameters of Methods
- Return types and thrown exceptions are **not** considered to be a part of the method signature, nor are the names of parameters; they are ignored by the compiler for checking method uniqueness.

**Overriding (Run-Time Polymorphism, Dynamic Polymorphism)**

- In Java, Overriding is a feature that allows a subclass or child class to provide a specific implementation of a method that is already provided by one of its super-classes or parent classes.
- When a method in a subclass has the same name, the same parameters or signature, and the same return type(or sub-type) as a method in its super-class, then the method in the subclass is said to override the method in the super-class.
- The version of a method that is executed will be determined by the object that is used to invoke it. If an object of a parent class is used to invoke the method, then the version in the parent class will be executed, but if an object of the subclass is used to invoke the method, then the version in the child class will be executed. In other words, it is the type of the object being referred to (not the type of the reference variable) that determines which version of an overridden method will be executed.

## Java Object-Oriented Programming (OOP) Concepts

**Access Modifier**

- Defines the access type of the method i.e. from where it can be accessed in your application. In Java, there are 4 types of access specifiers:
  - `public`: Accessible in all classes in your application.
  - `protected`: Accessible within the package in which it is defined and in its subclass(es) (including subclasses declared outside the package).
  - `private`: Accessible only within the class in which it is defined.
  - `default` (declared/defined without using any modifier): Accessible within the same class and package within which its class is defined.

**Return Type**

- The data type of the value returned by the method or void if it does not return a value.

**Method Name**

- The rules for field names apply to method names as well, but the convention is a little different.

**Parameter list**

- Comma-separated list of the input parameters that are defined, preceded by their data type, within the enclosed parentheses. If there are no parameters, you must use empty parentheses ().

**Exception list**

- The exceptions you expect the method to throw. You can specify these exception(s).

**Method body**

- It is the block of code, enclosed between braces, that you need to execute to perform your intended operations.

## Object-Oriented Programming (OOP) versus Procedure-Oriented Programming

**OOP promotes code reusability**

- By using objects and classes, you can create reusable components, leading to less duplication and more efficient development.

**OOP enhances code organization**

- It provides a clear and logical structure, making the code easier to understand, maintain, and debug.

**OOP supports the DRY (Don’t Repeat Yourself) principle**

- This principle encourages minimizing code repetition, leading to cleaner, more maintainable code. Common functionalities are placed in a single location and reused, reducing redundancy.

**OOP enables faster development**

- By reusing existing code and creating modular components, OOP allows for quicker and more efficient application development

## References

1. [Object Oriented Programming (OOPs) Concept in Java!](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/)
1. [Object-Oriented Programming in Java – A Beginner's Guide!](https://www.freecodecamp.org/news/object-oriented-programming-concepts-java/)
1. [Intro to Object Oriented Programming - Crash Course!](https://youtu.be/SiBw7os-_zI?si=9zsxwrVIOMgToPb7)
