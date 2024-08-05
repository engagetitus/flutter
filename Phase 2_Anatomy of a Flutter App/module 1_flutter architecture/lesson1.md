# Lesson 1: Overview of Flutter Architecture

## Overview

Introduction to the basic architecture of a Flutter app.

### Key Concepts

- Flutter Framework Overview 🧩
- Widgets: Building Blocks of Flutter 🏗️
- The Flutter Rendering Process 🎨

## Flutter Framework Overview 🧩

Flutter is an open-source UI software development toolkit created by Google. It is used to develop applications for Android, iOS, Linux, Mac, Windows, Google Fuchsia, and the web from a single codebase.

## Widgets: Building Blocks of Flutter 🏗️

- **Widgets** are the central class hierarchy in the Flutter framework. Everything in Flutter is a widget, including layout models and UI controls.

  ```dart
  // Example of a simple widget
  class MyWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Text('Hello, Flutter!');  // A text widget that displays 'Hello, Flutter!'
    }
  }

  ```

## The Flutter Rendering Process 🎨

The Flutter rendering process includes the following steps:

- Building: Flutter builds a widget tree.
- Layout: Determines the size and position of each widget.
- Painting: Draws the widget on the screen.
