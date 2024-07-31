
# Module 4: Cloud Firestore

## Lesson 3: Firestore CRUD Operations

### Creating and Writing Data to Firestore

```dart
Future<void> addUser(String uid, String name, String email) async {
  await FirebaseFirestore.instance.collection('users').doc(uid).set({
    'name': name,
    'email': email,
  });
}
```

### Reading Data from Firestore

```dart

Future<DocumentSnapshot> getUser(String uid) async {
  return await FirebaseFirestore.instance.collection('users').doc(uid).get();
}
```

### Updating Firestore Documents

```dart

Future<void> updateUser(String uid, String name) async {
  await FirebaseFirestore.instance.collection('users').doc(uid).update({
    'name': name,
  });
}
```

### Deleting Firestore Documents

```dart

Future<void> deleteUser(String uid) async {
  await FirebaseFirestore.instance.collection('users').doc(uid).delete();
}
```
