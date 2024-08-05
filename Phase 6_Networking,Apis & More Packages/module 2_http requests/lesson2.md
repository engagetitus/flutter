# Lesson 2: Making POST Requests

Overview: POST requests are used to send data to a server, such as submitting a form.

## Key Concepts

- Making POST Requests 🌐
- Handling Responses 📝
- Making POST Requests 🌐

## Making a simple POST request

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
          title: Text('HTTP POST Request Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: _makePostRequest,
            child: Text('Make POST Request'),
          ),
        ),
      ),
    );
  }

  void _makePostRequest() async {
    // Data to be sent in the POST request
    final response = await http.post(
      Uri.parse('https://jsonplaceholder.typicode.com/posts'),
      body: {'title': 'foo', 'body': 'bar', 'userId': '1'},
    );

    // Checking if the request was successful
    if (response.statusCode == 201) {
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

http.post sends a POST request to the specified URL with the provided body.

The response is checked for success (status code 201) and then printed.
