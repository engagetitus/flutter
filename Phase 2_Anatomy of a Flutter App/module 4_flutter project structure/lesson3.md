
# Lesson 3: Working with Assets

- **Overview**: How to add and use assets in a Flutter project.
- **Key Concepts**:
  - Adding Images and Fonts 🖼️
  - Using Images in Flutter 📸
  - Using Custom Fonts 🖋️

# Adding Images and Fonts 🖼️

- To add images, create an `images` directory in the root of your project and add your images.
- To add fonts, create a `fonts` directory in the root of your project and add your font files.

# Using Images in Flutter 📸

- Reference the images in `pubspec.yaml` and use them in your code.

  ```yaml
  flutter:
    assets:
      - images/my_image.png

  ```

## Using Custom Fonts 🖋️

Reference the fonts in pubspec.yaml and use them in your code.

```yaml

flutter:
  fonts:
    - family: CustomFont
      fonts:
        - asset: fonts/CustomFont-Regular.ttf
```

```dart

Text(
  'Custom Font Text',
  style: TextStyle(
    fontFamily: 'CustomFont',
  ),
)
```
