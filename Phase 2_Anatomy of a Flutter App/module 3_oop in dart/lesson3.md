
# Lesson 3: Constructors in Dart

- **Overview**: Understanding different types of constructors in Dart.
- **Key Concepts**:
  - Default Constructor 🏗️
  - Named Constructors 🔄
  - Factory Constructors 🏭

# Default Constructor 🏗️

- A default constructor is automatically created if no other constructor is defined.

  ```dart
  class Animal {
    String name;

    // Default constructor
    Animal(this.name);
  }

  var dog = Animal('Dog');

  ```
