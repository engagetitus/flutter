
# Module 8: Firebase Analytics

## Lesson 3: Logging Custom Events

### Implementing Custom Event Logging

```dart
FirebaseAnalytics analytics = FirebaseAnalytics.instance;

void logCustomEvent() {
  analytics.logEvent(
    name: 'custom_event',
    parameters: <String, dynamic>{
      'string': 'string_value',
      'int': 42,
      'long': 12345678910,
      'double': 42.0,
      'bool': true,
    },
  );
}
```

### Using Predefined Events

Firebase Analytics provides predefined events for common app interactions such as login, sign_up, purchase, etc.

``` dart

analytics.logLogin(loginMethod: 'email');
```

Analyzing Event Data in Firebase Console
Navigate to the Firebase Console.
Go to the Analytics section.
View event data and user properties.
