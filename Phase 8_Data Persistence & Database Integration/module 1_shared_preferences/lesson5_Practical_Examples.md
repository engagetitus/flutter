
# Practical Examples of Shared Preferences

## Example 1: User Login Session
### Storing User Session Data
When a user logs in, store their session data.

```dart
void _login(String username) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('username', username);
}
```

### Retrieving User Session Data
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

## Example 2: Storing User Preferences
### Storing Preferences
Save user preferences, such as theme choice or notification settings.

```dart
void _savePreferences(bool isDarkMode) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setBool('isDarkMode', isDarkMode);
}
```

### Retrieving Preferences
Load user preferences when the app starts.

```dart
void _loadPreferences() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  bool isDarkMode = prefs.getBool('isDarkMode') ?? false;
  // Apply the theme
}
```

## Example 3: Saving Form Data
### Storing Form Data
Save form data temporarily to resume later.

```dart
void _saveFormData(String name, String email) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('name', name);
  await prefs.setString('email', email);
}
```

### Retrieving Form Data
Load saved form data when returning to the form.

```dart
void _loadFormData() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String name = prefs.getString('name') ?? '';
  String email = prefs.getString('email') ?? '';
  // Populate form fields
}
```
