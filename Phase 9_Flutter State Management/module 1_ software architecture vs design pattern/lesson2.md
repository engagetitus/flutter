
#### Lesson 2: Introduction to Design Patterns


# Module 1: Software Architecture vs Design Pattern

## Lesson 2: Introduction to Design Patterns

### What are Design Patterns?
Design Patterns are typical solutions to common problems in software design. They are like blueprints that can be customized to solve a recurring design problem in your code.

### Types of Design Patterns
1. **Creational Patterns**: Deal with object creation mechanisms.
   - **Singleton Pattern**
   - **Factory Method Pattern**
2. **Structural Patterns**: Deal with object composition.
   - **Adapter Pattern**
   - **Composite Pattern**
3. **Behavioral Patterns**: Deal with object collaboration.
   - **Observer Pattern**
   - **Strategy Pattern**

### Example: Singleton Pattern in Dart
```dart
class Singleton {
  Singleton._privateConstructor();
  static final Singleton instance = Singleton._privateConstructor();
}
