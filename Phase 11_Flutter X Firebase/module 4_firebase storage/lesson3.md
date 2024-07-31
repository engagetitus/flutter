
# Module 5: Firebase Storage

## Lesson 3: Uploading Files

### Implementing File Upload in Flutter

```dart
import 'package:firebase_storage/firebase_storage.dart';
import 'dart:io';

Future<void> uploadFile(File file) async {
  try {
    await FirebaseStorage.instance
        .ref('uploads/${file.path.split('/').last}')
        .putFile(file);
  } catch (e) {
    print(e.toString());
  }
}
```

### Handling Upload Progress and Errors

```dart

UploadTask uploadTask = FirebaseStorage.instance
    .ref('uploads/${file.path.split('/').last}')
    .putFile(file);

uploadTask.snapshotEvents.listen((TaskSnapshot snapshot) {
  print('Progress: ${(snapshot.bytesTransferred / snapshot.totalBytes) * 100} %');
}, onError: (e) {
  print(uploadTask.lastSnapshot.bytesTransferred);
  if (e.code == 'permission-denied') {
    print('User does not have permission to upload to this reference.');
  }
});
```
