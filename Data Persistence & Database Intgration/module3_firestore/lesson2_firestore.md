# Session 2: Firebase Firestore Basics 

## Firestore Setup
1. Add `cloud_firestore` to your `pubspec.yaml` file.

```yaml
dependencies:
  cloud_firestore: ^3.1.5
```

2. Run `flutter pub get` to install the package.
3. Initialize Firestore in your Flutter app.

```dart
import 'package:cloud_firestore/cloud_firestore.dart';

FirebaseFirestore firestore = FirebaseFirestore.instance;
```

## CRUD Operations

### Create
```dart
Future<void> addUser(String userId, String name, int age) async {
  await firestore.collection('users').doc(userId).set({
    'name': name,
    'age': age,
  });
}
```

### Read
```dart
Future<DocumentSnapshot> getUser(String userId) async {
  return await firestore.collection('users').doc(userId).get();
}

Stream<QuerySnapshot> getUsers() {
  return firestore.collection('users').snapshots();
}
```

### Update
```dart
Future<void> updateUser(String userId, String name, int age) async {
  await firestore.collection('users').doc(userId).update({
    'name': name,
    'age': age,
  });
}
```

### Delete
```dart
Future<void> deleteUser(String userId) async {
  await firestore.collection('users').doc(userId).delete();
}
```