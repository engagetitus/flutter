
# Module 3: Firebase Authentication

## Lesson 4: Managing User Sessions

### Persisting User Sessions

Firebase Authentication automatically persists user sessions between app restarts. No additional code is needed for basic session persistence.

### Handling User Sign-Outs

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

### Implementing Password Reset Functionality

1. Enable password reset in the Firebase Console.
2. Implement the password reset functionality in your Flutter app:

```dart

Future<void> resetPassword(String email) async {
  try {
    await _auth.sendPasswordResetEmail(email: email);
  } catch (e) {
    print(e.toString());
  }
}
```

### TASK : Verifying Email
