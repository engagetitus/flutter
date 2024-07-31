
# Module 3: Firebase Authentication

## Lesson 3: Social Authentication

### Configuring Google Sign-In

1. In the Firebase Console, enable Google Sign-In.
2. Add the necessary dependencies to your `pubspec.yaml` file:

   ```yaml
   dependencies:
     google_sign_in: latest_version
    ```

### Implementing Google Sign-In in Flutter

``` dart
import 'package:google_sign_in/google_sign_in.dart';

final GoogleSignIn _googleSignIn = GoogleSignIn();

Future<User?> signInWithGoogle() async {
  try {
    final GoogleSignInAccount? googleUser = await _googleSignIn.signIn();
    final GoogleSignInAuthentication googleAuth =
        await googleUser!.authentication;

    final AuthCredential credential = GoogleAuthProvider.credential(
      accessToken: googleAuth.accessToken,
      idToken: googleAuth.idToken,
    );

    UserCredential result = await _auth.signInWithCredential(credential);
    return result.user;
  } catch (e) {
    print(e.toString());
    return null;
  }
}
```

### Adding Other Social Providers (Facebook, Twitter, etc.)

- Enable the desired authentication providers in the Firebase Console.
- Follow the setup instructions provided by Firebase for each provider.
- Implement the respective authentication flows in your Flutter app.
