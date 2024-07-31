
# Module 6: Cloud Functions

## Lesson 3: Firestore Triggers

### Writing Firestore Trigger Functions

```javascript
exports.userCreated = functions.firestore
    .document('users/{userId}')
    .onCreate((snap, context) => {
      const newValue = snap.data();
      console.log('New user created:', newValue);
    });
```

### Handling Firestore Document Changes

```javascript

exports.userUpdated = functions.firestore
    .document('users/{userId}')
    .onUpdate((change, context) => {
      const newValue = change.after.data();
      const previousValue = change.before.data();
      console.log('User updated:', newValue);
      console.log('Previous data:', previousValue);
    });
```

### Implementing Firestore Delete Triggers

```javascript

exports.userDeleted = functions.firestore
    .document('users/{userId}')
    .onDelete((snap, context) => {
      const deletedValue = snap.data();
      console.log('User deleted:', deletedValue);
    });
```
