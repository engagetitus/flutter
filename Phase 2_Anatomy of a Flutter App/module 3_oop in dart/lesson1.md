# Lesson 1: Introduction to Object-Oriented Programming

Overview: Basic concepts of Object-Oriented Programming (OOP).

## Key Concepts

Classes and Objects 📦
Inheritance 🧬
Polymorphism 🧩
markdown

## Classes and Objects 📦

- **Classes** are blueprints for creating objects (instances).

  ```dart
  // Defining a class
  class Animal {
    String name;
    int age;

    // Constructor
    Animal(this.name, this.age);

    // Method
    void speak() {
      print('$name makes a sound.');
    }
  }

  // Creating an object
  var dog = Animal('Dog', 5);
  dog.speak();  // Output: Dog makes a sound.

## Inheritance 🧬

Inheritance allows a class to inherit properties and methods from another class.

``` dart

// Parent class
class Animal {
  String name;
  Animal(this.name);
  void speak() {
    print('$name makes a sound.');
  }
}

// Child class
class Dog extends Animal {
  Dog(String name) : super(name);

  @override
  void speak() {
    print('$name barks.');
  }
}

var dog = Dog('Dog');
dog.speak();  // Output: Dog barks.
Polymorphism 🧩
Polymorphism allows objects to be treated as instances of their parent class.
dart

// Polymorphism example
Animal myAnimal = Dog('Dog');
myAnimal.speak();  // Output: Dog barks.
```
