# Lesson 3: Advanced Usage

**Objective:** Explore more advanced usage scenarios of Hive.

**Topics Covered:**

- Using Hive models.
- Custom adapters.
- Encryption.

## Using Hive Models

1. **Create a model class and annotate it with `HiveType` and `HiveField`:**

    ```dart
    import 'package:hive/hive.dart';

    part 'user.g.dart';

    @HiveType(typeId: 0)
    class User extends HiveObject {
      @HiveField(0)
      String name;

      @HiveField(1)
      int age;

      User({required this.name, required this.age});
    }
    ```

2. **Generate the type adapter for the model class:**

    Run the following command to generate the `user.g.dart` file:

    ```sh
    flutter packages pub run build_runner build
    ```

3. **Register the adapter:**

    ```dart
    void main() async {
      await Hive.initFlutter();
      Hive.registerAdapter(UserAdapter());

      runApp(MyApp());
    }
    ```

4. **Use the model in Hive:**

    ```dart
    var userBox = await Hive.openBox<User>('userBox');
    await userBox.put('user1', User(name: 'John Doe', age: 30));
    User? user = userBox.get('user1');
    ```

## Custom Adapters

1. **Create an adapter for the model:**

    ```dart
    class UserAdapter extends TypeAdapter<User> {
      @override
      final typeId = 0;

      @override
      User read(BinaryReader reader) {
        return User(
          name: reader.readString(),
          age: reader.readInt(),
        );
      }

      @override
      void write(BinaryWriter writer, User obj) {
        writer.writeString(obj.name);
        writer.writeInt(obj.age);
      }
    }
    ```

## Encryption

To securely store sensitive data, you can use Hive's built-in encryption support:

1. **Generate a secure encryption key:**

    ```dart
    import 'dart:convert';
    import 'dart:typed_data';
    import 'package:crypto/crypto.dart';

    Uint8List generateKey(String password) {
      final key = sha256.convert(utf8.encode(password)).bytes;
      return Uint8List.fromList(key);
    }

    final encryptionKey = generateKey('your-secure-password');
    ```

2. **Open an encrypted box:**

    ```dart
    var encryptedBox = await Hive.openBox('secureBox', encryptionCipher: HiveAesCipher(encryptionKey));
    ```

### Complete App with UI

Below is an updated example of a Flutter app that uses Hive with models, custom adapters, and encryption. It includes a UI that handles these operations.

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
  Hive.registerAdapter(UserAdapter());

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HiveExample(),
    );
  }
}

@HiveType(typeId: 0)
class User extends HiveObject {
  @HiveField(0)
  String name;

  @HiveField(1)
  int age;

  User({required this.name, required this.age});
}

class HiveExample extends StatefulWidget {
  @override
  _HiveExampleState createState() => _HiveExampleState();
}

class _HiveExampleState extends State<HiveExample> {
  late Box<User> userBox;
  TextEditingController _nameController = TextEditingController();
  TextEditingController _ageController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _openBox();
  }

  Future<void> _openBox() async {
    userBox = await Hive.openBox<User>('userBox');
    setState(() {});
  }

  Future<void> _addUser(String name, int age) async {
    await userBox.put('user1', User(name: name, age: age));
    setState(() {});
  }

  User? _getUser() {
    return userBox.get('user1');
  }

  Future<void> _deleteUser() async {
    await userBox.delete('user1');
    setState(() {});
  }

  void _showUserDialog() {
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Enter User'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: _ageController,
              decoration: InputDecoration(labelText: 'Age'),
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
              final name = _nameController.text;
              final age = int.tryParse(_ageController.text) ?? 0;

              _addUser(name, age);
              _nameController.clear();
              _ageController.clear();
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
    final user = _getUser();

    return Scaffold(
      appBar: AppBar(
        title: Text('Hive Example'),
        actions: [
          IconButton(
            icon: Icon(Icons.add),
            onPressed: _showUserDialog,
          ),
        ],
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Name: ${user?.name ?? 'No user saved'}'),
            Text('Age: ${user?.age ?? 'No age saved'}'),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _deleteUser,
              child: Text('Delete User'),
            ),
          ],
        ),
      ),
    );
  }
}
```
