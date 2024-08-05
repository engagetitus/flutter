Lesson 3: Error Handling in Async Code
Overview: Error handling is crucial for making robust applications. In asynchronous code, we handle errors using try, catch, and finally.

Key Concepts:

Using try, catch, finally in async functions 🚨
Handling Stream Errors 📡
Using try, catch, finally in async functions 🚨

Just like real life, things can go wrong in your code. You can handle these errors gracefully using try, catch, and finally.

Error handling with async functions:
dart

// Function that simulates fetching data and throws an error
Future<String> fetchDataWithError() async {
  await Future.delayed(Duration(seconds: 2));
  // Simulating an error
  throw 'An error occurred!';
}

void main() async {
  try {
    // Trying to fetch data
    String data = await fetchDataWithError();
    print(data);
  } catch (e) {
    // Catching and printing the error
    print('Error: $e'); // Outputs 'Error: An error occurred!'
  } finally {
    // Cleanup code, runs whether there was an error or not
    print('Cleanup code here');
  }
}
Explanation:

try block contains the code that might throw an error.
catch block handles the error.
finally block runs regardless of whether an error occurred or not, useful for cleanup.
Handling Stream Errors 📡

You can also handle errors in streams, which might be necessary if the stream data source fails.

Error handling with Streams:
dart

// Stream generator function that throws an error at value 3
Stream<int> countStreamWithError(int max) async* {
  for (int i = 1; i <= max; i++) {
    if (i == 3) {
      // Throwing an error when i is 3
      throw 'An error at value $i';
    }
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

void main() {
  Stream<int> stream = countStreamWithError(5);

  // Listening to the stream and handling errors
  stream.listen(
    (value) {
      print(value);
    },
    onError: (error) {
      print('Error: $error'); // Outputs 'Error: An error at value 3'
    },
  );
}
Explanation:

onError parameter of stream.listen handles errors emitted by the stream.
Errors in streams are common when dealing with unreliable data sources like network connections.