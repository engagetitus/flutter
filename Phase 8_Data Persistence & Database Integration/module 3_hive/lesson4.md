# Lesson 4: Practical Example

**Objective:** Build a marks entry system using Hive.

## Marks Entry System

1. **Define the Marks Model:**

    ```dart
    import 'package:hive/hive.dart';

    part 'marks.g.dart';

    @HiveType(typeId: 1)
    class Marks extends HiveObject {
      @HiveField(0)
      String subject;

      @HiveField(1)
      int marks;

      Marks({required this.subject, required this.marks});
    }
    ```

2. **Generate the Type Adapter for the Model:**

    Run the following command to generate the `marks.g.dart` file:

    ```sh
    flutter packages pub run build_runner build
    ```

3. **Register the Adapter:**

    ```dart
    void main() async {
      await Hive.initFlutter();
      Hive.registerAdapter(MarksAdapter());

      runApp(MyApp());
    }
    ```

4. **Use the Model in Hive:**

    ```dart
    var marksBox = await Hive.openBox<Marks>('marksBox');

    // Add a mark
    await marksBox.put('math', Marks(subject: 'Math', marks: 95));

    // Retrieve a mark
    Marks? mathMarks = marksBox.get('math');

    // Update a mark
    await marksBox.put('math', Marks(subject: 'Math', marks: 98));

    // Delete a mark
    await marksBox.delete('math');
    ```

### Complete App with UI

Below is a complete example of a Flutter app that uses Hive to manage marks entry. It includes a UI that handles these operations.

#### Dependencies

First, add the Hive dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  hive: ^2.0.0
  hive_flutter: ^1.0.0

dev_dependencies:
  hive_generator: ^1.0.0
  build_runner: ^2.0.0
```

#### Main Application Code

```dart
import 'package:flutter/material.dart';
import 'package:hive/hive.dart';
import 'package:hive_flutter/hive_flutter.dart';

part 'main.g.dart';

void main() async {
  await Hive.initFlutter();
  Hive.registerAdapter(MarksAdapter());

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

@HiveType(typeId: 1)
class Marks extends HiveObject {
  @HiveField(0)
  String subject;

  @HiveField(1)
  int marks;

  Marks({required this.subject, required this.marks});
}

class MarksEntryScreen extends StatefulWidget {
  @override
  _MarksEntryScreenState createState() => _MarksEntryScreenState();
}

class _MarksEntryScreenState extends State<MarksEntryScreen> {
  late Box<Marks> marksBox;
  TextEditingController _subjectController = TextEditingController();
  TextEditingController _marksController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _openBox();
  }

  Future<void> _openBox() async {
    marksBox = await Hive.openBox<Marks>('marksBox');
    setState(() {});
  }

  Future<void> _addMarks(String subject, int marks) async {
    await marksBox.put(subject, Marks(subject: subject, marks: marks));
    setState(() {});
  }

  Marks? _getMarks(String subject) {
    return marksBox.get(subject);
  }

  Future<void> _deleteMarks(String subject) async {
    await marksBox.delete(subject);
    setState(() {});
  }

  void _showMarksDialog({Marks? marks}) {
    if (marks != null) {
      _subjectController.text = marks.subject;
      _marksController.text = marks.marks.toString();
    } else {
      _subjectController.clear();
      _marksController.clear();
    }

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text(marks == null ? 'Enter Marks' : 'Edit Marks'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
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
          ],
        ),
        actions: [
          TextButton(
            onPressed: () {
              Navigator.of(context).pop();
            },
            child: Text('Cancel'),
          ),
          ElevatedButton(
            onPressed: () {
              final subject = _subjectController.text;
              final marks = int.tryParse(_marksController.text) ?? 0;

              if (marks != null) {
                _addMarks(subject, marks);
              }

              _subjectController.clear();
              _marksController.clear();
              Navigator.of(context).pop();
            },
            child: Text('Save'),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Marks Entry'),
        actions: [
          IconButton(
            icon: Icon(Icons.add),
            onPressed: () => _showMarksDialog(),
          ),
        ],
      ),
      body: ValueListenableBuilder(
        valueListenable: marksBox.listenable(),
        builder: (context, Box<Marks> box, _) {
          if (box.values.isEmpty) {
            return Center(child: Text('No marks entered'));
          }

          return ListView.builder(
            itemCount: box.values.length,
            itemBuilder: (context, index) {
              Marks marks = box.getAt(index) as Marks;
              return Dismissible(
                key: Key(marks.subject),
                background: Container(color: Colors.red),
                onDismissed: (direction) {
                  _deleteMarks(marks.subject);
                },
                child: ListTile(
                  title: Text('Subject: ${marks.subject}'),
                  subtitle: Text('Marks: ${marks.marks}'),
                  trailing: IconButton(
                    icon: Icon(Icons.edit),
                    onPressed: () => _showMarksDialog(marks: marks),
                  ),
                ),
              );
            },
          );
        },
      ),
    );
  }
}
```

### Additional Examples

Here are three more examples of how to use Hive for different applications.

### Example 1: Todo List App

1. **Define the Todo Model:**

    ```dart
    @HiveType(typeId: 2)
    class Todo {
      @HiveField(0)
      String title;

      @HiveField(1)
      String description;

      @HiveField(2)
      bool isComplete;

      Todo({
        required this.title,
        required this.description,
        this.isComplete = false,
      });
    }
    ```

2. **Register the Adapter:**

    ```dart
    Hive.registerAdapter(TodoAdapter());
    ```

3. **Use the Model in Hive:**

    ```dart
    var todoBox = await Hive.openBox<Todo>('todoBox');

    // Add a todo
    await todoBox.put('todo1', Todo(title: 'Buy groceries', description: 'Milk, Eggs, Bread'));

    // Retrieve a todo
    Todo? todo1 = todoBox.get('todo1');

    // Update a todo
    todo1!.isComplete = true;
    await todo1.save();

    // Delete a todo
    await todoBox.delete('todo1');
    ```

### Example 2: Contact List App

1. **Define the Contact Model:**

    ```dart
    @HiveType(typeId: 3)
    class Contact {
      @HiveField(0)
      String name;

      @HiveField(1)
      String phoneNumber;

      Contact({required this.name, required this.phoneNumber});
    }
    ```

2. **Register the Adapter:**

    ```dart
    Hive.registerAdapter(ContactAdapter());
    ```

3. **Use the Model in Hive:**

    ```dart
    var contactBox = await Hive.openBox<Contact>('contactBox');

    // Add a contact
    await contactBox.put('contact1', Contact(name: 'John Doe', phoneNumber: '123-456-7890'));

    // Retrieve a contact
    Contact? contact1 = contactBox.get('contact1');

    // Update a contact
    contact1!.phoneNumber = '098-765-4321';
    await contact1.save();

    // Delete a contact
    await contactBox.delete('contact1');
    ```

### Example 3: Notes App

1. **Define the Note Model:**

    ```dart
    @HiveType(typeId: 4)
    class Note {
      @HiveField(0)
      String title;

      @HiveField(1)
      String content;

      @HiveField(2)
      DateTime date;

      Note({
        required this.title,
        required this.content,
        required this.date,
      });
    }
    ```

2. **Register the Adapter:**

    ```dart
    Hive.registerAdapter(NoteAdapter());
    ```

3. **Use the Model in Hive:**

    ```dart
    var noteBox = await Hive.openBox<Note>('noteBox');

    // Add a note
    await noteBox.put('note1', Note(
      title: 'Meeting Notes',
      content: 'Discuss project timelines and deliverables',
      date: DateTime.now(),
    ));

    // Retrieve a note
    Note? note1 = noteBox.get

    ('note1');

    // Update a note
    note1!.content = 'Updated content';
    await note1.save();

    // Delete a note
    await noteBox.delete('note1');
    ```
