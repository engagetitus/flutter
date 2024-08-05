Lesson 2: Working with Streams
Overview: Streams are used to handle a sequence of asynchronous events. Unlike Future, which returns a single value, a Stream can deliver multiple values over time.

Key Concepts:

Basics of Streams 📡
Listening to Stream Data 🎧
Basics of Streams 📡

Think of a stream like a conveyor belt in a factory, where items (data) come down the line at different times.

Creating and using a simple Stream:
dart

// Stream generator function that emits numbers from 1 to max with a delay
Stream<int> countStream(int max) async* {
  for (int i = 1; i <= max; i++) {
    // Simulating some delay
    await Future.delayed(Duration(seconds: 1));
    // Yielding the current value
    yield i;
  }
}

void main() async {
  // Listening to the stream and printing values as they come
  await for (int value in countStream(5)) {
    print(value); // Outputs numbers from 1 to 5, one per second
  }
}
Explanation:

async* function generates a stream of integers.
yield keyword sends a value to the stream.
await for is used to process each value as it arrives.
Listening to Stream Data 🎧

You can listen to a stream to react to each value as it is emitted.

Listening to data from a Stream:
dart

void main() {
  // Getting the stream
  Stream<int> stream = countStream(5);

  // Listening to the stream
  stream.listen((value) {
    print(value); // Outputs numbers from 1 to 5, one per second
  });
}
Explanation:

stream.listen sets up a listener that runs the provided callback for each value emitted by the stream.