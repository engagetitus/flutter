
#### Lesson 4: Practical Examples with Assets
- **Overview**: Hands-on examples demonstrating the use of various assets.
- **Key Concepts**:
  - Combining Images, Icons, and Fonts 🧩
  - Building a Themed Application 🎨


# Combining Images, Icons, and Fonts 🧩
- **Creating a UI that combines images, icons, and fonts**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: CombinedAssetsScreen(),
      );
    }
  }

  class CombinedAssetsScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Combined Assets Example'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Image.asset('assets/images/my_image.png'), // Displaying an image from assets
              SizedBox(height: 20),
              Icon(
                Icons.favorite,
                color: Colors.red,
                size: 50.0,
              ), // Displaying a built-in icon
              SizedBox(height: 20),
              Text(
                'Hello, Flutter!',
                style: TextStyle(
                  fontFamily: 'CustomFont', // Applying a custom font
                  fontSize: 24,
                ),
              ),
            ],
          ),
        ),
      );
    }
  }
```
Building a Themed Application 🎨
Creating a Flutter application with a custom theme:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        primarySwatch: Colors.blue,
        textTheme: TextTheme(
          bodyText1: TextStyle(fontFamily: 'CustomFont'),
        ),
      ),
      home: ThemedApplicationScreen(),
    );
  }
}

class ThemedApplicationScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Themed Application Example'),
      ),
      body: Center(
        child: Text(
          'Hello, Themed Flutter!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```
