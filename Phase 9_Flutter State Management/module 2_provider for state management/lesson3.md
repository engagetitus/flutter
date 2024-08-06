# Module 2: Provider for State Management

## Lesson 3: Provider & Change Notifier to Manage State

### Understanding ChangeNotifier

`ChangeNotifier` is a class in the Flutter framework that provides change notification to its listeners. When the state changes, it notifies the listeners, which can then rebuild their widgets to reflect the new state. This is a key concept in managing state in Flutter applications.

### Using ChangeNotifier with Provider

The `Provider` package in Flutter allows for easy integration of `ChangeNotifier`. Here’s how you can use `ChangeNotifier` to manage state in your Flutter app.

### Difference Between `with` and `extends`

In Dart, `with` is used for mixins, which allows a class to use the properties and methods of another class without actually inheriting from it. `extends` is used for inheritance, where the child class inherits properties and methods from the parent class.

- `extends`: Used when a class inherits from another class. The child class can override the parent class's methods.
- `with`: Used to include mixins. A class can use multiple mixins, allowing for code reuse without inheritance.

Example:
```dart
class Animal {
  void breathe() {
    print("Animal is breathing");
  }
}

mixin Fly {
  void fly() {
    print("Flying");
  }
}

class Bird extends Animal with Fly {}

void main() {
  Bird bird = Bird();
  bird.breathe(); // From Animal
  bird.fly(); // From Fly
}
```

### Setting Up ChangeNotifier

Add the `provider` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  provider: ^6.0.0
```

### Basic Example

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MyApp(),
    ),
  );
}

class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Example')),
        body: Center(
          child: Consumer<Counter>(
            builder: (context, counter, child) {
              return Text('Count: ${counter.count}');
            },
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Provider.of<Counter>(context, listen: false).increment();
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

### Scenarios Using ChangeNotifier

#### 1. Dark Mode Toggle

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => ThemeNotifier(),
      child: MyApp(),
    ),
  );
}

class ThemeNotifier with ChangeNotifier {
  bool _isDarkMode = false;

  bool get isDarkMode => _isDarkMode;

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<ThemeNotifier>(
      builder: (context, themeNotifier, child) {
        return MaterialApp(
          theme: themeNotifier.isDarkMode ? ThemeData.dark() : ThemeData.light(),
          home: Scaffold(
            appBar: AppBar(
              title: Text('Dark Mode Example'),
              actions: [
                Switch(
                  value: themeNotifier.isDarkMode,
                  onChanged: (value) {
                    themeNotifier.toggleTheme();
                  },
                ),
              ],
            ),
            body: Center(
              child: Text('Toggle Dark Mode'),
            ),
          ),
        );
      },
    );
  }
}
```

#### 2. User Authentication

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => AuthNotifier(),
      child: MyApp(),
    ),
  );
}

class AuthNotifier with ChangeNotifier {
  bool _isLoggedIn = false;

  bool get isLoggedIn => _isLoggedIn;

  void login() {
    _isLoggedIn = true;
    notifyListeners();
  }

  void logout() {
    _isLoggedIn = false;
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<AuthNotifier>(
      builder: (context, authNotifier, child) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(
              title: Text('Auth Example'),
              actions: [
                IconButton(
                  icon: Icon(authNotifier.isLoggedIn ? Icons.logout : Icons.login),
                  onPressed: () {
                    authNotifier.isLoggedIn ? authNotifier.logout() : authNotifier.login();
                  },
                ),
              ],
            ),
            body: Center(
              child: authNotifier.isLoggedIn ? Text('Logged In') : Text('Logged Out'),
            ),
          ),
        );
      },
    );
  }
}
```

#### 3. Language Preference

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => LanguageNotifier(),
      child: MyApp(),
    ),
  );
}

class LanguageNotifier with ChangeNotifier {
  Locale _locale = Locale('en');

  Locale get locale => _locale;

  void setLocale(String languageCode) {
    _locale = Locale(languageCode);
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<LanguageNotifier>(
      builder: (context, languageNotifier, child) {
        return MaterialApp(
          locale: languageNotifier.locale,
          home: Scaffold(
            appBar: AppBar(title: Text('Language Example')),
            body: Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text('Current Language: ${languageNotifier.locale.languageCode}'),
                  ElevatedButton(
                    onPressed: () => languageNotifier.setLocale('en'),
                    child: Text('English'),
                  ),
                  ElevatedButton(
                    onPressed: () => languageNotifier.setLocale('es'),
                    child: Text('Spanish'),
                  ),
                ],
              ),
            ),
          ),
        );
      },
    );
  }
}
```

#### 4. Notifications

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => NotificationNotifier(),
      child: MyApp(),
    ),
  );
}

class NotificationNotifier with ChangeNotifier {
  List<String> _notifications = [];

  List<String> get notifications => _notifications;

  void addNotification(String notification) {
    _notifications.add(notification);
    notifyListeners();
  }

  void clearNotifications() {
    _notifications.clear();
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<NotificationNotifier>(
      builder: (context, notificationNotifier, child) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(
              title: Text('Notifications Example'),
              actions: [
                IconButton(
                  icon: Icon(Icons.clear_all),
                  onPressed: notificationNotifier.clearNotifications,
                ),
              ],
            ),
            body: Column(
              children: [
                Expanded(
                  child: ListView.builder(
                    itemCount: notificationNotifier.notifications.length,
                    itemBuilder: (context, index) {
                      return ListTile(
                        title: Text(notificationNotifier.notifications[index]),
                      );
                    },
                  ),
                ),
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: ElevatedButton(
                    onPressed: () {
                      notificationNotifier.addNotification('New Notification at ${DateTime.now()}');
                    },
                    child: Text('Add Notification'),
                  ),
                ),
              ],
            ),
          ),
        );
      },
    );
  }
}
```

### Comments and Insights

- **State Management:** By using `ChangeNotifier`, you can manage state efficiently by notifying listeners only when necessary. This reduces unnecessary rebuilds and improves performance.
- **Provider Integration:** The `Provider` package makes it easy to inject and access `ChangeNotifier` instances in the widget tree.
- **Scalability:** Using `ChangeNotifier` with `Provider` scales well for medium to large applications, keeping state management clean and maintainable.
- **Customization:** You can create multiple `ChangeNotifier` classes to handle different aspects of the application, like theme, authentication, language, and notifications, and use `MultiProvider` to manage them efficiently.

