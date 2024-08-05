
# Lesson 4: Practical Project Setup

- **Overview**: Hands-on session to set up a Flutter project with dependencies and assets.
- **Key Concepts**:
  - Creating a New Flutter Project 🆕
  - Adding Dependencies 📦
  - Adding and Using Assets 🖼️

# Creating a New Flutter Project 🆕

1. **Create a new project**:

  ```bash
  flutter create my_new_app
  cd my_new_app
  ```

## Adding Dependencies 📦

Edit pubspec.yaml to include the http package:

```yaml

dependencies:
  http: ^0.13.3
  ```

Run the following command:

```bash

flutter pub get
```

## Adding and Using Assets 🖼️

Create an images directory and add an image file.

Edit pubspec.yaml to include the image:

```yaml

flutter:
  assets:
    - images/my_image.png
```

Use the image in your code:

```dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Practical Project Setup'),
        ),
        body: Center(
          child: Image.asset('images/my_image.png'),  // Displaying the image
        ),
      ),
    );
  }
}
```
