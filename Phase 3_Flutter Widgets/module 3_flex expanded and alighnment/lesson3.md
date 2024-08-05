
# Lesson 3: Alignment in Flutter

- **Overview**: How to align widgets in Flutter using various properties.
- **Key Concepts**:
  - Align Widget 📐
  - MainAxisAlignment and CrossAxisAlignment 🔄
  - Using Alignment Property 🧭

# Align Widget 📐

- The `Align` widget is used to align its child within itself.

  ```dart
  Align(
    alignment: Alignment.center,
    child: Text('Centered Text'),
  )

## MainAxisAlignment and CrossAxisAlignment 🔄

**MainAxisAlignment**: Aligns children along the main axis.

```dart

Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: <Widget>[
    Text('Child 1'),
    Text('Child 2'),
    Text('Child 3'),
  ],
)
```

**CrossAxisAlignment**: Aligns children along the cross axis.

```dart

Column(
  crossAxisAlignment: CrossAxisAlignment.start,
  children: <Widget>[
    Text('Child 1'),
    Text('Child 2'),
    Text('Child 3'),
  ],
)
```

## Using Alignment Property 🧭

The alignment property is used to align widgets within containers.

```dart

Container(
  alignment: Alignment.bottomRight,
  child: Text('Bottom Right'),
)
```
