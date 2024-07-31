
# Cloud Messaging

## Sending Notifications

1. Add `firebase_messaging` to your `pubspec.yaml` file.

    ```yaml
    dependencies:
      firebase_messaging: ^14.0.0
    ```

2. Run `flutter pub get` to install the package.
3. Initialize Firebase Messaging in your Flutter app.

    ```dart
    import 'package:firebase_messaging/firebase_messaging.dart';

    FirebaseMessaging messaging = FirebaseMessaging.instance;

    void requestNotificationPermissions() async {
      NotificationSettings settings = await messaging.requestPermission();
      if (settings.authorizationStatus == AuthorizationStatus.authorized) {
        print('User granted permission');
      } else {
        print('User declined or has not accepted permission');
      }
    }
    ```

4. Handle incoming notifications.

    ```dart
    FirebaseMessaging.onMessage.listen((RemoteMessage message) {
      print('Received a message while in the foreground!');
      print('Message data: ${message.data}');

      if (message.notification != null) {
        print('Message also contained a notification: ${message.notification}');
      }
    });
    ```

## Firebase Analytics

### Tracking Events

1. Add `firebase_analytics` to your `pubspec.yaml` file.

    ```yaml
    dependencies:
      firebase_analytics: ^10.0.6
    ```

2. Run `flutter pub get` to install the package.
3. Initialize Firebase Analytics in your Flutter app.

    ```dart
    import 'package:firebase_analytics/firebase_analytics.dart';

    FirebaseAnalytics analytics = FirebaseAnalytics.instance;
    ```

4. Log custom events.

```dart
Future<void> logCustomEvent() async {
  await analytics.logEvent(
    name: 'custom_event',
    parameters: <String, dynamic>{
      'string': 'foo',
      'int': 42,
      'long': 1234567890,
      'double': 3.14159,
    },
  );
}
```

### Analyzing User Behavior

Use the Firebase Console to view analytics reports and analyze user behavior.
