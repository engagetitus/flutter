# Lesson 3: Advanced Usage

**Objective:** Explore more advanced usage scenarios of Shared Preferences.

**Topics Covered:**

- Handling different data types.
- Checking for existing keys.
- Clearing all data.
- Using Shared Preferences in a real app scenario.
- Performance considerations.

## Handling Different Data Types

Shared Preferences allows you to store various data types, including integers, doubles, booleans, and lists of strings.

### Saving and Retrieving Integers

```dart
Future<void> _saveInt(String key, int value) async {
  final prefs = await SharedPreferences.getInstance();
  prefs.setInt(key, value);
}

Future<int?> _getInt(String key) async {
  final prefs = await SharedPreferences.getInstance();
  return prefs.getInt(key);
}
```

## Saving and Retrieving Booleans

```dart
Future<void> _saveBool(String key, bool value) async {
  final prefs = await SharedPreferences.getInstance();
  prefs.setBool(key, value);
}

Future<bool?> _getBool(String key) async {
  final prefs = await SharedPreferences.getInstance();
  return prefs.getBool(key);
}
```

### Saving and Retrieving Lists of Strings

```dart
Future<void> _saveStringList(String key, List<String> value) async {
  final prefs = await SharedPreferences.getInstance();
  prefs.setStringList(key, value);
}

Future<List<String>?> _getStringList(String key) async {
  final prefs = await SharedPreferences.getInstance();
  return prefs.getStringList(key);
}
```

## Checking for Existing Keys

To check if a key exists in Shared Preferences, use the `containsKey` method.

```dart
Future<bool> _containsKey(String key) async {
  final prefs = await SharedPreferences.getInstance();
  return prefs.containsKey(key);
}

// Example usage
Future<void> checkKey() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  bool hasUsername = prefs.containsKey('username');
  if (hasUsername) {
    print('Username exists');
  } else {
    print('Username does not exist');
  }
}
```

## Clearing All Data

To clear all data stored in Shared Preferences, use the `clear` method.

```dart
Future<void> _clearAllData() async {
  final prefs = await SharedPreferences.getInstance();
  prefs.clear();
}

// Example usage
Future<void> clearData() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.clear();
}
```

## Real App Scenario: User Settings

### Saving and Retrieving User Settings

```dart
class UserSettings {
  Future<void> saveThemeMode(bool isDarkMode) async {
    final prefs = await SharedPreferences.getInstance();
    prefs.setBool('isDarkMode', isDarkMode);
  }

  Future<bool?> getThemeMode() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getBool('isDarkMode');
  }
}

// Example usage in a widget
class SettingsPage extends StatefulWidget {
  @override
  _SettingsPageState createState() => _SettingsPageState();
}

class _SettingsPageState extends State<SettingsPage> {
  late SharedPreferences prefs;
  late String username;

  @override
  void initState() {
    super.initState();
    _loadPreferences();
  }

  void _loadPreferences() async {
    prefs = await SharedPreferences.getInstance();
    setState(() {
      username = prefs.getString('username') ?? 'Guest';
    });
  }

  void _savePreferences() async {
    await prefs.setString('username', username);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Settings'),
      ),
      body: Column(
        children: [
          TextField(
            decoration: InputDecoration(labelText: 'Username'),
            onChanged: (value) {
              setState(() {
                username = value;
              });
            },
            onSubmitted: (value) {
              _savePreferences();
            },
          ),
          Text('Saved Username: $username'),
        ],
      ),
    );
  }
}
```

## Performance Considerations

- Shared Preferences are suitable for storing small amounts of data.
- For larger datasets or more complex data structures, consider using a local database like SQLite.
