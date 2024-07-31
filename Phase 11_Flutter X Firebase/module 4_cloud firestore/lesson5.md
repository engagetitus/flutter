
# Module 4: Cloud Firestore

## Lesson 4: Advanced Firestore Queries

### Filtering and Ordering Data

```dart
QuerySnapshot users = await FirebaseFirestore.instance
    .collection('users')
    .where('age', isGreaterThan: 18)
    .orderBy('age', descending: true)
    .get();
```

### Pagination in Firestore

```dart

Query usersQuery = FirebaseFirestore.instance.collection('users').limit(10);

DocumentSnapshot lastVisible;
usersQuery = usersQuery.startAfterDocument(lastVisible);
QuerySnapshot users = await usersQuery.get();
```

Real-time Updates with Firestore Snapshots

```dart

FirebaseFirestore.instance
    .collection('users')
    .snapshots()
    .listen((QuerySnapshot snapshot) {
  snapshot.docs.forEach((doc) {
    print(doc.data());
  });
});
```
