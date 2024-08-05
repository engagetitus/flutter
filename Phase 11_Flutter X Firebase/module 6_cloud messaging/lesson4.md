
### Lesson 4: Handling Notifications in Flutter


# Handling Notifications in Flutter

Handling incoming notifications in Flutter, both when the app is in the foreground and in the background.

## Receiving and Displaying Notifications

Use the `FirebaseMessaging` plugin to handle incoming messages.

```dart
import 'package:firebase_messaging/firebase_messaging.dart';
import 'package:flutter/material.dart';

class MessagingWidget extends StatefulWidget {
  @override
  _MessagingWidgetState createState() => _MessagingWidgetState();
}

class _MessagingWidgetState extends State<MessagingWidget> {
  final FirebaseMessaging _firebaseMessaging = FirebaseMessaging.instance;

  @override
  void initState() {
    super.initState();
    _firebaseMessaging.setForegroundNotificationPresentationOptions(alert: true, badge: true, sound: true);

    FirebaseMessaging.onMessage.listen((RemoteMessage message) {
      // Handle foreground messages
      showDialog(
        context: context,
        builder: (_) => AlertDialog(
          title: Text(message.notification?.title ?? 'No Title'),
          content: Text(message.notification?.body ?? 'No Body'),
        ),
      );
    });

    FirebaseMessaging.onMessageOpenedApp.listen((RemoteMessage message) {
      // Handle message when the app is brought to foreground from notification
      print('Message clicked!');
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('FCM Messages')),
      body: Center(child: Text('Listen for messages...')),
    );
  }
}

Handling Foreground and Background Messages
FCM provides hooks to manage messages when your app is in the background and when it resumes.

dart

FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);

Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  // Handle data messages in the background
  print('Handling a background message ${message.messageId}');
}
Customizing Notification Display
Customize how notifications are displayed in your app using local notifications.

dart

import 'package:flutter_local_notifications/flutter_local_notifications.dart';

FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();

// Initialization settings for Android and iOS
var initializationSettingsAndroid = AndroidInitializationSettings('app_icon');
var initializationSettingsIOS = IOSInitializationSettings();
var initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid,
    iOS: initializationSettingsIOS);

flutterLocalNotificationsPlugin.initialize(initializationSettings);

// Show notification with custom settings
void showNotification() {
  var androidPlatformChannelSpecifics = AndroidNotificationDetails(
    'your_channel_id', 'your_channel_name', 'your_channel_description',
    importance: Importance.max, priority: Priority.high, showWhen: false);
  var iOSPlatformChannelSpecifics = IOSNotificationDetails();
  var platformChannelSpecifics = NotificationDetails(
    android: androidPlatformChannelSpecifics, iOS: iOSPlatformChannelSpecifics);

  flutterLocalNotificationsPlugin.show(
    0, 'Custom Title', 'Custom Body', platformChannelSpecifics,
    payload: 'Custom Payload');
}
Advanced Practical Example: SMS Notification App
markdown

# Advanced Practical Example: SMS Notification App

Create an app where messages sent to a user trigger an SMS notification using Cloud Functions and FCM.

## Cloud Function to Send SMS on Message

```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
const twilio = require('twilio');

admin.initializeApp();

const twilioClient = new twilio('TWILIO_ACCOUNT_SID', 'TWILIO_AUTH_TOKEN');

exports.sendSMSNotification = functions.firestore.document('messages/{messageId}').onCreate((snap, context) => {
  const messageData = snap.data();

  return twilioClient.messages.create({
    body: `New message from ${messageData.sender}: ${messageData.text}`,
    to: messageData.receiverPhone,  // Assuming 'receiverPhone' is stored in the document
    from: 'YOUR_TWILIO_PHONE_NUMBER'
  }).then((message) => console.log(message.sid)).catch((error) => console.error(error));
});
This function is triggered whenever a new message document is created in Firestore, sending an SMS to the recipient's phone number via Twilio.

Integration in Flutter App
The Flutter app subscribes to notification topics and handles them accordingly, displaying alerts or updating the UI based on the content of the message.
