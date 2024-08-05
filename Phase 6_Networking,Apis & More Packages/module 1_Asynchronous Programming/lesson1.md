Lesson 1: Introduction to Asynchronous Programming
Overview: Asynchronous programming allows your code to handle tasks that might take some time, like fetching data from the internet, without freezing your app. In Dart, we use async and await to make this process easier and more readable.

Key Concepts:

Basics of async and await ⏳
Handling Futures in Dart 🔮
Basics of async and await ⏳

Imagine you are cooking multiple dishes at once. While one dish is simmering, you can start preparing another. Similarly, asynchronous programming allows your code to do other things while waiting for a task to complete.

Using async and await in Dart:
dart

// The main function can also be asynchronous
void main() async {
  print('Before the delay');
  // The await keyword pauses the execution until the future is completed
  await Future.delayed(Duration(seconds: 2));
  print('After the delay');
}
Explanation:

async keyword marks a function as asynchronous.
await pauses the function execution until the Future completes.
In this example, there's a 2-second delay before printing 'After the delay'.
Handling Futures in Dart 🔮

A Future represents a potential value or error that will be available at some time in the future.

Working with Futures:
dart

// Function that returns a Future with some delay
Future<String> fetchData() {
  return Future.delayed(Duration(seconds: 2), () => 'Data fetched');
}

void main() async {
  print('Fetching data...');
  // Waiting for the future to complete
  String data = await fetchData();
  // Data fetched will be printed after 2 seconds
  print(data); 
}
Explanation:

fetchData simulates a network request by delaying for 2 seconds and then returning a string.
await is used to pause the execution until the future completes.