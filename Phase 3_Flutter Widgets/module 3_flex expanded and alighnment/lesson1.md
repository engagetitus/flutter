# Lesson 1: Introduction to Flex Widgets

- **Overview**: Understanding flex widgets and their properties.
- **Key Concepts**:
  - What are Flex Widgets? 🔀
  - Flex Properties 📐
  - FlexDirection: Row vs Column ➡️⬇️

## What are Flex Widgets? 🔀

- Flex widgets are used to create flexible layouts that can adapt to different screen sizes and orientations. Examples include `Row` and `Column`.

## Flex Properties 📐

- **mainAxisAlignment**: How the children should be placed along the main axis.
- **crossAxisAlignment**: How the children should be placed along the cross axis.

## FlexDirection: Row vs Column ➡️⬇️

- **Row**: Lays out its children horizontally.
- **Column**: Lays out its children vertically.

  ```dart
  Row(
    mainAxisAlignment: MainAxisAlignment.center,
    children: <Widget>[
      Text('Child 1'),
      Text('Child 2'),
      Text('Child 3'),
    ],
  )

  Column(
    mainAxisAlignment: MainAxisAlignment.center,
    children: <Widget>[
      Text('Child 1'),
      Text('Child 2'),
      Text('Child 3'),
    ],
  )

  ```
