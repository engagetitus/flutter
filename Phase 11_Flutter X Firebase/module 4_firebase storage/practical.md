# Session 3: Firebase Storage (4 hours)

1. Add `firebase_storage` to your `pubspec.yaml` file.

    ```yaml
    dependencies:
      firebase_storage: ^10.2.7
    ```

2. Run `flutter pub get` to install the package.
3. Initialize Firebase Storage in your Flutter app.

    ```dart
    import 'package:firebase_storage/firebase_storage.dart';

    FirebaseStorage storage = FirebaseStorage.instance;
    ```

4. Upload a file to Firebase Storage.

```dart
Future<void> uploadFile(File file, String filePath) async {
  try {
    await storage.ref(filePath).putFile(file);
  } catch (e) {
    print('Error uploading file: $e');
  }
}
```

## File Download

```dart
Future<File> downloadFile(String filePath, File localFile) async {
  try {
    await storage.ref(filePath).writeToFile(localFile);
    return localFile;
  } catch (e) {
    print('Error downloading file: $e');
    return null;
  }
}
```

## Managing Files

```dart
Future<void> deleteFile(String filePath) async {
  try {
    await storage.ref(filePath).delete();
  } catch (e) {
    print('Error deleting file: $e');
  }
}
```
