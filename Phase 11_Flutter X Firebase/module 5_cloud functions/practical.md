
# Firebase Cloud Functions

## Introduction to Cloud Functions

Firebase Cloud Functions allow you to run backend code in response to events triggered by Firebase features and HTTPS requests.

## Setting up Cloud Functions

1. Install Firebase CLI.
2. Initialize Cloud Functions in your project.

    ```bash
    firebase init functions
    ```

3. Write a simple function.

    ```javascript
    const functions = require('firebase-functions');

    exports.helloWorld = functions.https.onRequest((request, response) => {
      response.send("Hello from Firebase!");
    });
    ```

4. Deploy the function.

```bash
firebase deploy --only functions
```

## Writing and Deploying Functions

### HTTP Functions

```javascript
exports.addMessage = functions.https.onRequest(async (req, res) => {
  const original = req.query.text;
  const writeResult = await admin.firestore().collection('messages').add({original: original});
  res.json({result: `Message with ID: ${writeResult.id} added.`});
});
```

### Firestore Triggers

```javascript
exports.makeUppercase = functions.firestore.document('/messages/{documentId}')
  .onCreate((snap, context) => {
    const original = snap.data().original;
    const uppercase = original.toUpperCase();
    return snap.ref.set({uppercase}, {merge: true});
  });
```
