
# Module 5: Firebase Storage

## Lesson 4: Downloading and Displaying Files

### Implementing File Download in Flutter

```dart
Future<void> downloadFile(String filePath) async {
  try {
    String downloadURL = await FirebaseStorage.instance
        .ref('uploads/$filePath')
        .getDownloadURL();
    // Use the download URL to display the file
  } catch (e) {
    print(e.toString());
  }
}
```

### Displaying Images from Firebase Storage

```dart

Image.network(downloadURL);
```

### Handling Download Errors

``` dart

try {
  String downloadURL = await FirebaseStorage.instance
      .ref('uploads/$filePath')
      .getDownloadURL();
  // Display the file
} catch (e) {
  print('Error: $e');
}
```
