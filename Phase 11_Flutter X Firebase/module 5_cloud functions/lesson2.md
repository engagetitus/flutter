# Module 6: Cloud Functions

## Lesson 2: Setting up Cloud Functions
Learn how to write and deploy a simple Cloud Function to respond to HTTP requests.


### Initializing Firebase Functions

1. Install Firebase CLI: `npm install -g firebase-tools`
2. Initialize Firebase in your project: `firebase init functions`
3. Deploy functions: `firebase deploy --only functions`

## Writing a Simple HTTP Cloud Function

Here's how you can create a basic HTTP-triggered function in JavaScript:

```javascript
const functions = require('firebase-functions');

// Defines a Cloud Function that responds to HTTP requests.
exports.helloWorld = functions.https.onRequest((request, response) => {
  // Sends a simple response to the client.
  response.send("Hello from Firebase!");
});
```

This function listens for HTTP requests and sends back a greeting. It's a basic example of how to handle incoming HTTP requests with Cloud Functions.

Deploying Your Function
To deploy this function to Firebase, you will use the Firebase CLI:

bash

firebase deploy --only functions
This command sends your code to Google's servers and makes the function accessible over the web.

Python Equivalent
For those who prefer Python, here’s how to achieve the same with Python using the functions-framework:

python

import functions_framework

@functions_framework.http
def hello_world(request):
    return 'Hello from Firebase!', 200
To deploy a Python function, ensure you have the functions-framework Python library installed and use the Google Cloud CLI:

bash

gcloud functions deploy hello_world --runtime python39 --trigger-http --allow-unauthenticated
