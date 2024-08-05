
#### Lesson 2: Working with Icons
- **Overview**: Using icons in Flutter applications.
- **Key Concepts**:
  - Built-in Icons 🛠️
  - Custom Icons 🎨


# Built-in Icons 🛠️
- **Using Flutter's built-in icons**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: BuiltInIconsScreen(),
      );
    }
  }

  class BuiltInIconsScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Built-in Icons Example'),
        ),
        body: Center(
          child: Icon(
            Icons.favorite, // Using a built-in icon
            color: Colors.red,
            size: 50.0,
          ),
        ),
      );
    }
  }
```
Custom Icons 🎨
Using custom icons in your Flutter project:

Add your custom icon files to the assets directory.
Update your pubspec.yaml file to include the assets.
yaml

flutter:
  assets:
    - assets/icons/
Displaying a custom icon:

``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CustomIconsScreen(),
    );
  }
}

class CustomIconsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Icons Example'),
      ),
      body: Center(
        child: Image.asset('assets/icons/custom_icon.png'), // Displaying a custom icon from assets
      ),
    );
  }
}
```
