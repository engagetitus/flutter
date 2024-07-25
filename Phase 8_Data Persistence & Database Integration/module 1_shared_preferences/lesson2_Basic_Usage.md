
# Basic Usage of Shared Preferences

## Storing Data
You can store data using various methods provided by the `SharedPreferences` class.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();

// Store a string value
await prefs.setString('username', 'JohnDoe');

// Store an integer value
await prefs.setInt('age', 25);

// Store a boolean value
await prefs.setBool('isLoggedIn', true);

// Store a double value
await prefs.setDouble('height', 5.9);

// Store a list of strings
await prefs.setStringList('favorites', ['Apple', 'Banana', 'Cherry']);
```

## Retrieving Data
To retrieve data, use the corresponding getter methods.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();

// Retrieve a string value
String username = prefs.getString('username') ?? 'Guest';

// Retrieve an integer value
int age = prefs.getInt('age') ?? 0;

// Retrieve a boolean value
bool isLoggedIn = prefs.getBool('isLoggedIn') ?? false;

// Retrieve a double value
double height = prefs.getDouble('height') ?? 0.0;

// Retrieve a list of strings
List<String> favorites = prefs.getStringList('favorites') ?? [];
```

## Removing Data
To remove data, use the `remove` method.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
await prefs.remove('username');
```
