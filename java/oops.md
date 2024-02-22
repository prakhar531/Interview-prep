# OOPs (Object-Oriented Programming System)

Object means a real-world entity such as a pen, chair, table, computer, watch, etc.
Object-Oriented Programming, or OOPs, is a programming paradigm that implements the concept of objects in the program.
It aims to provide an easier solution to real-world problems by implementing real-world entities such as inheritance, abstraction, polymorphism, etc. in programming.
OOPs concept is widely used in many popular languages like Java, Python, C++, etc.

## Why OOPs?

1. The main advantage of OOP is better manageable code that covers the following:

2. The overall understanding of the software is increased as the distance between the language spoken by developers and that spoken by users.

3. Object orientation eases maintenance by the use of encapsulation. The OOPs paradigm is mainly useful for relatively big software.

It simplifies software development and maintenance by providing some concepts.

- Object
- Class
- Inheritance
- Polymorphism
- Abstraction
- Encapsulation
  The main aim of object-oriented programming is to implement real-world entities.

## Object

An object is an instance of a class.
Data members and methods of a class cannot be used directly. We need to create an object (or instance) of the class to use them.
An entity that has state and behavior is known as an object e.g., chair, bike, marker, pen, table, car, etc.
It can be physical or logical (tangible and intangible). The example of an intangible object is the banking system.

### An object has three characteristics:

- **State**: represents the data (value) of an object.

- **Behavior**: represents the behavior (functionality) of an object such as deposit, withdraw, etc.

- **Identity**: An object identity is typically implemented via a unique ID. The value of the ID is not visible to the external user. However, it is used internally by the JVM to identify each object uniquely.

An object is an instance of a class. A class is a template or blueprint from which objects are created.

## Class

A class is a building block of Object Oriented Programs.
It is a user-defined data type that contains the **data members** and **member functions** that operate on the data members.
A class is a group of objects which have common properties.
It is a template or blueprint from which objects are created.
It is a logical entity. It can't be physical.

A class in Java can contain:

- Fields
- Methods: expose the behavior of an object.
- Constructors
- Blocks
- Nested class and interface

## What are the main features of OOPs?

The main feature of the OOPs, also known as 4 pillars or basic principles of OOPs are as follows:

1. Encapsulation
2. Data Abstraction
3. Polymorphism
4. Inheritance

### Instance variable in Java

A variable which is created inside the class but outside the method is known as an instance variable.
Instance variable doesn't get memory at compile time. It gets memory at runtime when an object or instance is created. That is why it is known as an instance variable.

### new keyword in Java

The new keyword is used to allocate memory at runtime. All objects get memory in Heap memory area.

There are 3 ways to initialize object in Java.

- By reference variable
- By method
- By constructor

## Advantages of OOPs

- OOPs provides enhanced code reusability.
- The code is easier to maintain and update.
- It provides better data security by restricting data access and avoiding unnecessary exposure.
- Fast to implement and easy to redesign resulting in minimizing the complexity of an overall program.

## Disadvantages of OOPs

- The programmer should be well-skilled and should have excellent thinking in terms of objects as everything is treated as an object in OOPs.
- Proper planning is required because OOPs is a little bit tricky.
- OOPs concept is not suitable for all kinds of problems.
- The length of the programs is much larger in comparison to the procedural approach.

### What is the difference between a structure and a class in C++?

The structure is also a user-defined datatype in C++ similar to the class with the following differences:

- The major difference between a structure and a class is that in a structure, the members are set to public by default while in a class, members are private by default.
- The other difference is that we use struct for declaring structure and class for declaring a class in C++.

## What is Constructor?

A constructor is a block of code that initializes the newly created object.
A constructor resembles an instance method but it’s not a method as it doesn’t have a return type.
It generally is the method having the same name as the class but in some languages, it might differ. For example:
In python, a constructor is named **init**.
In C++ and Java, the constructor is named the same as the class name.

### What are the various types of constructors?

The most common classification of constructors includes:

- Default Constructor
- Non-Parameterized Constructor
- Parameterized Constructor
- Copy Constructor

1. **Default Constructor**
   The default constructor is a constructor that doesn’t take any arguments. It is a non-parameterized constructor that is automatically defined by the compiler when no explicit constructor definition is provided.

It initializes the data members to their default values.

2. **Non-Parameterized Constructor**
   It is a user-defined constructor having no arguments or parameters.

````java
    class Student {
          String name;
          String surname;
          int rollNo;
        Student()
        {
            System.out.println("Non-parameterized contructor is called");
        }
    }
    ```

````

3. **Parameterized Constructor**
   The constructors that take some arguments are known as parameterized constructors.

````java
      class Student {
            String name;
            String surname;
            int rollNo;
          Student(String studentName, String studentSurname, int studentRollNo)
          {
              System.out.println("Constructor with argument is called");
          }
      }
      ```
````

4. **Copy Constructor**
   A copy constructor is a member function that initializes an object using another object of the same class.

````java
    class Student {
        String name, surname; int rollNo;
        Student(Student student) // copy constructor
        {
            this.name = student.name;
            this.surname=student.surname;
              this.rollNo= student.rollNo;
        }
    }
    ```
````

### What is Garbage Collection(GC)?

GC is an implementation of automatic memory management. The Garbage collector frees up space occupied by objects that are no longer in existence.
