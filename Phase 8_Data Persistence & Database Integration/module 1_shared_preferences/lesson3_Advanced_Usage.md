
# Advanced Usage of Shared Preferences

## Checking for Keys
To check if a key exists in the Shared Preferences, use the `containsKey` method.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
bool hasUsername = prefs.containsKey('username');
```

## Clearing All Data
To clear all data stored in Shared Preferences, use the `clear` method.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
await prefs.clear();
```

## Using Shared Preferences in Widgets
You can use Shared Preferences within your widgets to store and retrieve data dynamically.

```dart
class SettingsPage extends StatefulWidget {
  @override
  _SettingsPageState createState() => _SettingsPageState();
}

class _SettingsPageState extends State<SettingsPage> {
  SharedPreferences prefs;
  String username;

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
