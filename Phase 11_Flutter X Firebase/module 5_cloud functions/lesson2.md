# Module 6: Cloud Functions

## Lesson 2: Setting up Cloud Functions

### Initializing Firebase Functions

1. Install Firebase CLI: `npm install -g firebase-tools`
2. Initialize Firebase in your project: `firebase init functions`
3. Deploy functions: `firebase deploy --only functions`

### Writing Your First Cloud Function

```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
admin.initializeApp();

exports.helloWorld = functions.https.onRequest((request, response) => {
  response.send("Hello from Firebase!");
});
