# Lesson 2: Encapsulation and Abstraction

- **Overview**: Understanding encapsulation and abstraction in OOP.
- **Key Concepts**:
  - Encapsulation 🔒
  - Abstraction 🌐

## Encapsulation 🔒

- **Encapsulation** is the bundling of data with methods that operate on that data.

  ```dart
  class Person {
    String _name;  // Private variable

    // Getter
    String get name => _name;

    // Setter
    set name(String name) {
      _name = name;
    }
  }

  var person = Person();
  person.name = 'John';
  print(person.name);  // Output: John

  ```

## Abstraction 🌐

Abstraction hides the complex implementation details and shows only the essential features of the object.

```dart

// Abstract class
abstract class Animal {
  void speak();  // Abstract method
}

class Dog extends Animal {
  @override
  void speak() {
    print('Dog barks.');
  }
}

var dog = Dog();
dog.speak();  // Output: Dog barks.
```
