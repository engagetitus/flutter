
# Module 7: Cloud Messaging

## Lesson 3: Receiving Messages

### Handling Message Reception in Flutter

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

FirebaseMessaging messaging = FirebaseMessaging.instance;

void main() {
  runApp(MyApp());
  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    print('Got a message whilst in the foreground!');
    print('Message data: ${message.data}');

    if (message.notification != null) {
      print('Message also contained a notification: ${message.notification}');
    }
  });
}
```

### Displaying Notifications

Implement local notifications to display incoming messages using packages like `flutter_local_notifications`.
