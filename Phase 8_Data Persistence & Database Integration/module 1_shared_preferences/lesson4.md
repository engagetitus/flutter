# Lesson 4: Practical Example - Marks Entry System

**Objective:** Build a marks entry system using Shared Preferences.

**Topics Covered:**

- Storing marks for different subjects.
- Retrieving marks for a specific subject.
- Retrieving all marks.
- Displaying marks in a UI.

## Marks Entry System

In this lesson, we will build a marks entry system that allows users to save, retrieve, and display marks for different subjects using Shared Preferences.

### Saving and Retrieving Marks

```dart
class MarksEntry {
  Future<void> saveMarks(String subject, int marks) async {
    final prefs = await SharedPreferences.getInstance();
    prefs.setInt(subject, marks);
  }

  Future<int?> getMarks(String subject) async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getInt(subject);
  }

  Future<Map<String, int>> getAllMarks() async {
    final prefs = await SharedPreferences.getInstance();
    final keys = prefs.getKeys();
    Map<String, int> marks = {};
    for (String key in keys) {
      marks[key] = prefs.getInt(key) ?? 0;
    }
    return marks;
  }
}
```

## Practical Examples of Shared Preferences

### Example 1: User Login Session

#### Storing User Session Data

When a user logs in, store their session data.

```dart
void _login(String username) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('username', username);
}
```

#### Retrieving User Session Data

When the app starts, check if the user is logged in.

```dart
void _checkUserSession() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String username = prefs.getString('username') ?? 'Guest';
  if (username != 'Guest') {
    // Navigate to home page
  } else {
    // Show login page
  }
}
```

### Example 2: Storing User Preferences

#### Storing Preferences

Save user preferences, such as theme choice or notification settings.

```dart
void _savePreferences(bool isDarkMode) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setBool('isDarkMode', isDarkMode);
}
```

#### Retrieving Preferences

Load user preferences when the app starts.

```dart
void _loadPreferences() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  bool isDarkMode = prefs.getBool('isDarkMode') ?? false;
  // Apply the theme
}
```

### Example 3: Saving Form Data

#### Storing Form Data

Save form data temporarily to resume later.

```dart
void _saveFormData(String name, String email) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('name', name);
  await prefs.setString('email', email);
}
```

#### Retrieving Form Data

Load saved form data when returning to the form.

```dart
void _loadFormData() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String name = prefs.getString('name') ?? '';
  String email = prefs.getString('email') ?? '';
  // Populate form fields
}
```

## Complete Code with UI

Here is the complete code for the marks entry system, including the UI.

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MarksEntryScreen(),
    );
  }
}

class MarksEntryScreen extends StatefulWidget {
  @override
  _MarksEntryScreenState createState() => _MarksEntryScreenState();
}

class _MarksEntryScreenState extends State<MarksEntryScreen> {
  TextEditingController _subjectController = TextEditingController();
  TextEditingController _marksController = TextEditingController();
  Map<String, int> _marks = {};

  @override
  void initState() {
    super.initState();
    _loadAllMarks();
  }

  Future<void> _saveMarks(String subject, int marks) async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _marks[subject] = marks;
    });
    prefs.setInt(subject, marks);
  }

  Future<void> _loadAllMarks() async {
    final prefs = await SharedPreferences.getInstance();
    final keys = prefs.getKeys();
    Map<String, int> marks = {};
    for (String key in keys) {
      marks[key] = prefs.getInt(key) ?? 0;
    }
    setState(() {
      _marks = marks;
    });
  }

  Future<void> _clearMarks() async {
    final prefs = await SharedPreferences.getInstance();
    prefs.clear();
    setState(() {
      _marks.clear();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Marks Entry System'),
        actions: [
          IconButton(
            icon: Icon(Icons.delete_forever),
            onPressed: _clearMarks,
          )
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          children: [
            TextField(
              controller: _subjectController,
              decoration: InputDecoration(labelText: 'Subject'),
            ),
            TextField(
              controller: _marksController,
              decoration: InputDecoration(labelText: 'Marks'),
              keyboardType: TextInputType.number,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                if (_subjectController.text.isNotEmpty &&
                    _marksController.text.isNotEmpty) {
                  int marks = int.parse(_marksController.text);
                  _saveMarks(_subjectController.text, marks);
                  _subjectController.clear();
                  _marksController.clear();
                }
              },
              child: Text('Save Marks'),
            ),
            SizedBox(height: 20),
            Expanded(
              child: ListView.builder(
                itemCount: _marks.length,
                itemBuilder: (context, index) {
                  String subject = _marks.keys.elementAt(index);
                  int marks = _marks[subject]!;
                  return ListTile(
                    title: Text('$subject: $marks'),
                  );
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
