# Lesson 3: Parsing JSON Data

Overview: JSON (JavaScript Object Notation) is a common format for sending and receiving data in web applications.

## Key Concepts

- Parsing JSON Responses 🧩
- Using dart:convert Package 📦
- Parsing JSON Responses 🧩

## Parsing a JSON response

```dart

import 'dart:convert'; // Importing dart:convert for JSON decoding
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('JSON Parsing Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: _fetchAndParseData,
            child: Text('Fetch and Parse JSON'),
          ),
        ),
      ),
    );
  }

  void _fetchAndParseData() async {
    // Making a GET request to a dummy API
    final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

    // Checking if the request was successful
    if (response.statusCode == 200) {
      // Parsing the response body as JSON
      final data = json.decode(response.body);
      // Accessing the title from the parsed JSON
      print('Title: ${data['title']}');
    } else {
      // Handling errors
      print('Request failed with status: ${response.statusCode}');
    }
  }
}
```

### Explanation

json.decode parses the JSON string into a Dart map.

Accessing the parsed data is done using the map's keys.
