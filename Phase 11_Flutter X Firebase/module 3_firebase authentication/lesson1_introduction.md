# Session 1: Introduction to Firebase

## Overview of Firebase

Firebase is a platform developed by Google for creating mobile and web applications. It provides a suite of cloud services to help you build, improve, and grow your app.

## Firebase Console Setup

1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Click on "Add Project" and follow the setup instructions.
3. Register your app (iOS/Android) and download the `google-services.json` or `GoogleService-Info.plist` file.
4. Add the configuration file to your Flutter project.

## Firebase Authentication

### Email/Password Authentication

```dart
import 'package:firebase_auth/firebase_auth.dart';

Future<UserCredential> signInWithEmailPassword(String email, String password) async {
  return await FirebaseAuth.instance.signInWithEmailAndPassword(email: email, password: password);
}

Future<UserCredential> signUpWithEmailPassword(String email, String password) async {
  return await FirebaseAuth.instance.createUserWithEmailAndPassword(email: email, password: password);
}
```

### Third-party Authentication (Google)

```dart
import 'package:firebase_auth/firebase_auth.dart';
import 'package:google_sign_in/google_sign_in.dart';

Future<UserCredential> signInWithGoogle() async {
  final GoogleSignInAccount googleUser = await GoogleSignIn().signIn();
  final GoogleSignInAuthentication googleAuth = await googleUser.authentication;
  final credential = GoogleAuthProvider.credential(
    accessToken: googleAuth.accessToken,
    idToken: googleAuth.idToken,
  );
  return await FirebaseAuth.instance.signInWithCredential(credential);
}
```
