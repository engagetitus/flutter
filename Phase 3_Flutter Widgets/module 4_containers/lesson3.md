
# Lesson 3: Adding Decorations to Container

- **Overview**: How to add decorations such as borders, shadows, and gradients to `Container` widgets.
- **Key Concepts**:
  - Adding Borders 🖌️
  - Adding Shadows 🌫️
  - Adding Gradients 🌈

## Adding Borders 🖌️

Use the `decoration` property to add borders to a container.

  ```dart
  Container(
    decoration: BoxDecoration(
      border: Border.all(color: Colors.black, width: 2),
    ),
    child: Text('Container with Border'),
  )
   ```

## Adding Shadows 🌫️

Use the boxShadow property to add shadows to a container.

 ``` dart

Container(
  decoration: BoxDecoration(
    color: Colors.white,
    boxShadow: [
      BoxShadow(
        color: Colors.grey,
        offset: Offset(4, 4),
        blurRadius: 10,
      ),
    ],
  ),
  child: Text('Container with Shadow'),
)
 ```

## Adding Gradients 🌈

Use the gradient property to add gradients to a container.

 ```dart

Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Colors.blue, Colors.green],
    ),
  ),
  child: Text('Container with Gradient'),
)
 ```
