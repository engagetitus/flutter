# Lesson 5: Best Practices

**Objective:** Learn the best practices for using Shared Preferences.

## Best Practices

1. **Keep Data Simple:** Use Shared Preferences for simple key-value pairs only.
2. **Limit Usage:** Avoid storing large amounts of data. For larger datasets, use a local database like SQLite.
3. **Data Validation:** Always validate data before saving or retrieving to ensure data integrity.
4. **Use Async Functions:** Always use asynchronous functions to prevent blocking the UI.

### Data Size

- **Small Data:** Use Shared Preferences for small data sizes only.
- **Large Data:** For larger datasets, use a local database like SQLite.

### Data Types

- **Primitive Data Types:** Store only primitive data types (strings, ints, doubles, booleans, lists of strings).
- **Complex Data:** For complex data structures, consider serialization or using a database.

### Key Management

- **Consistent Naming:** Use consistent and descriptive key names.
- **Key Constants:** Define keys as constants to avoid typos and ensure consistency.

```dart
class PreferencesKeys {
  static const String username = 'username';
  static const String isLoggedIn = 'isLoggedIn';
}
```

### Performance

- **Avoid Frequent Reads/Writes:** Minimize the number of reads and writes to Shared Preferences to avoid performance issues.
- **Batch Operations:** Perform batch operations where possible.

### Security

- **Sensitive Data:** Avoid storing sensitive data like passwords in Shared Preferences. Use secure storage solutions for sensitive data.

### Error Handling

- **Default Values:** Always provide default values when retrieving data to handle cases where keys might not exist.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
String username = prefs.getString('username') ?? 'Guest';
```

### Testing

- **Unit Tests:** Write unit tests to verify the correct functioning of Shared Preferences operations.
- **Mocking:** Use mocking frameworks to mock Shared Preferences in tests.

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() {
  test('Test Shared Preferences', () async {
    SharedPreferences.setMockInitialValues({});
    SharedPreferences prefs = await SharedPreferences.getInstance();
    await prefs.setString('username', 'JohnDoe');
    expect(prefs.getString('username'), 'JohnDoe');
  });
}
```

## Example

### Saving User Settings

Save user settings using a map and handle different data types appropriately.

```dart
Future<void> saveUserSettings(Map<String, dynamic> settings) async {
  final prefs = await SharedPreferences.getInstance();
  settings.forEach((key, value) {
    if (value is String) {
      prefs.setString(key, value);
    } else if (value is int) {
      prefs.setInt(key, value);
    } else if (value is bool) {
      prefs.setBool(key, value);
    }
  });
}
```
