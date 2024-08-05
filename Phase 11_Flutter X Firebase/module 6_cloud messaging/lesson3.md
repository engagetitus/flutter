
# Module 7: Cloud Messaging


### Lesson 3: Sending Notifications


# Sending Notifications

Learn how to send notifications directly from the Firebase Console and programmatically via Cloud Functions.

## Sending Notifications from Firebase Console

The Firebase Console allows you to send simple push notifications directly to your users without writing any backend code.

## Implementing Topic-Based Notifications

Subscribe users to topics based on their interests or actions, and send notifications to these topics.

```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
admin.initializeApp();

exports.sendTopicNotification = functions.firestore.document('profiles/{profileId}').onUpdate((change, context) => {
  const profileData = change.after.data();

  const message = {
    notification: {
      title: 'Profile Viewed',
      body: `${profileData.username}'s profile has been viewed!`
    },
    topic: 'profile-updates'
  };

  return admin.messaging().send(message);
});

Sending Data Messages
Data messages can be sent to carry information that isn't directly displayed to users but can be processed by the app in the background.

javascript

exports.sendDataMessage = functions.https.onCall((data, context) => {
  const payload = {
    data: {
      taskId: '123',
      status: 'complete'
    },
    topic: 'task-updates'
  };

  return admin.messaging().send(payload);
});