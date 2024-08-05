
#### Lesson 3: Handling Form Submission
- **Overview**: Techniques for handling form submission in Flutter.
- **Key Concepts**:
  - Submitting Forms 📨
  - Displaying Submission Feedback 🗣️


# Submitting Forms 📨
- **Handling form submission**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: FormSubmissionScreen(),
      );
    }
  }

  class FormSubmissionScreen extends StatelessWidget {
    final _formKey = GlobalKey<FormState>();
    final TextEditingController _controller = TextEditingController();

    void _submitForm() {
      if (_formKey.currentState!.validate()) {
        print('Form submitted: ${_controller.text}');
      }
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Form Submission Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Form(
            key: _formKey,
            child: Column(
              children: [
                TextFormField(
                  controller: _controller,
                  decoration: InputDecoration(labelText: 'Enter text'),
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Please enter some text';
                    }
                    return null;
                  },
                ),
                SizedBox(height: 20),
                ElevatedButton(
                  onPressed: _submitForm,
                  child: Text('Submit'),
                ),
              ],
            ),
          ),
        ),
      );
    }
  }
```
Displaying Submission Feedback 🗣️
Showing feedback after form submission:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SubmissionFeedbackScreen(),
    );
  }
}

class SubmissionFeedbackScreen extends StatelessWidget {
  final _formKey = GlobalKey<FormState>();
  final TextEditingController _controller = TextEditingController();

  void _submitForm(BuildContext context) {
    if (_formKey.currentState!.validate()) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Form submitted: ${_controller.text}')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Submission Feedback Example'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _controller,
                decoration: InputDecoration(labelText: 'Enter text'),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Please enter some text';
                  }
                  return null;
                },
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () => _submitForm(context),
                child: Text('Submit'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
