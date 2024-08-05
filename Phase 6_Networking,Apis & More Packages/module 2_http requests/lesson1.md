# Lesson 1: Introduction to HTTP Requests

Overview: Making HTTP requests is a common task in many apps, especially those that interact with web services. Flutter provides the http package to simplify this process.

## Key Concepts

- Installing the http package 📦
- Making GET Requests 🌐
- Installing the http package 📦

Before making HTTP requests, you need to add the http package to your project.

### Update your pubspec.yaml file

```yaml

dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3 # Adding the http package
```

## Making GET Requests 🌐

Making a simple GET request:

```dart

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
          title: Text('HTTP GET Request Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: _makeGetRequest,
            child: Text('Make GET Request'),
          ),
        ),
      ),
    );
  }

  void _makeGetRequest() async {
    // Making a GET request to a dummy API
    final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

    // Checking if the request was successful
    if (response.statusCode == 200) {
      // Parsing the response body
      print('Response data: ${response.body}');
    } else {
      // Handling errors
      print('Request failed with status: ${response.statusCode}');
    }
  }
}
```

### Explanation

http.get makes a GET request to the specified URL.  
The response is checked for success and then printed.
