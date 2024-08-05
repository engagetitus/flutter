
### Module 6: Working with Assets

#### Lesson 1: Introduction to Assets
- **Overview**: Basics of working with assets in Flutter.
- **Key Concepts**:
  - Adding Images to Your Project 🖼️
  - Using `Image` Widget 📸


# Adding Images to Your Project 🖼️
- **Including images in your Flutter project**:
  - Add your image files to an `assets` directory in your project.
  - Update your `pubspec.yaml` file to include the assets.
  ```yaml
  flutter:
    assets:
      - assets/images/
```
Using Image Widget 📸
Displaying an image using the Image widget:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ImageAssetScreen(),
    );
  }
}

class ImageAssetScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Asset Example'),
      ),
      body: Center(
        child: Image.asset('assets/images/my_image.png'), // Displaying an image from assets
      ),
    );
  }
}
```
