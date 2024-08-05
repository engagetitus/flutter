
#### Lesson 3: Using Fonts
- **Overview**: Adding and using custom fonts in Flutter.
- **Key Concepts**:
  - Adding Fonts to Your Project 📝
  - Applying Custom Fonts 🎨


# Adding Fonts to Your Project 📝
- **Including custom fonts in your Flutter project**:
  - Add your font files to an `assets/fonts` directory in your project.
  - Update your `pubspec.yaml` file to include the fonts.
  ```yaml
  flutter:
    fonts:
      - family: CustomFont
        fonts:
          - asset: assets/fonts/CustomFont-Regular.ttf
          - asset: assets/fonts/CustomFont-Bold.ttf
            weight: 700
```
Applying Custom Fonts 🎨
Using custom fonts in your Flutter application:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CustomFontScreen(),
    );
  }
}

class CustomFontScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Fonts Example'),
      ),
      body: Center(
        child: Text(
          'Hello, Flutter!',
          style: TextStyle(
            fontFamily: 'CustomFont', // Applying the custom font
            fontSize: 24,
          ),
        ),
      ),
    );
  }
}
```
