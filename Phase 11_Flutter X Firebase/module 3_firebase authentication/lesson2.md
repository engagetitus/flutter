# Module 3: Firebase Authentication

## Lesson 2: Email/Password Authentication

### Setting up Email/Password Authentication

1. Go to the Firebase Console and select your project.
2. Navigate to the Authentication section.
3. Click on the "Sign-in method" tab.
4. Enable "Email/Password" authentication.

### Implementing Sign-Up Functionality

```dart
import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  final FirebaseAuth _auth = FirebaseAuth.instance;

  Future<User?> signUp(String email, String password) async {
    try {
      UserCredential result = await _auth.createUserWithEmailAndPassword(
          email: email, password: password);
      return result.user;
    } catch (e) {
      print(e.toString());
      return null;
    }
  }
}
```

### Implementing Login Functionality

``` dart

Future<User?> signIn(String email, String password) async {
  try {
    UserCredential result = await _auth.signInWithEmailAndPassword(
        email: email, password: password);
    return result.user;
  } catch (e) {
    print(e.toString());
    return null;
  }
}
```

### Implementing Logout Functionality

```dart

Future<void> signOut() async {
  try {
    return await _auth.signOut();
  } catch (e) {
    print(e.toString());
    return null;
  }
}
```
