
# Lesson 1: Introduction to Riverpod

# What is Riverpod?

Riverpod is a state management solution for Flutter applications that provides a more powerful and flexible way to manage state compared to Provider. It offers compile-time safety, a simpler syntax, and enhanced debugging capabilities.

## Benefits of Using Riverpod

- Type safety
- Easily testable
- Improved code readability
- No need for BuildContext

### Setting Up Riverpod

Add the riverpod dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_riverpod: ^1.0.0
```

### Basic Example

```dart

import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

final counterProvider = StateProvider<int>((ref) => 0);

void main() {
  runApp(ProviderScope(child: MyApp()));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Riverpod Example')),
        body: Center(
          child: Consumer(builder: (context, watch, child) {
            final count = watch(counterProvider).state;
            return Text('Count: $count');
          }),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            context.read(counterProvider).state++;
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

### Practical Example: Shopping Cart

```dart

import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Cart Provider
final cartProvider = StateNotifierProvider<Cart, List<Product>>((ref) => Cart());

class Cart extends StateNotifier<List<Product>> {
  Cart() : super([]);

  void addProduct(Product product) {
    state = [...state, product];
  }

  void removeProduct(Product product) {
    state = state.where((item) => item != product).toList();
  }

  double get total {
    return state.fold(0, (sum, item) => sum + item.price);
  }
}

void main() {
  runApp(ProviderScope(child: MyApp()));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Riverpod Cart Example')),
        body: Column(
          children: [
            Expanded(
              child: ProductList(),
            ),
            CartTotal(),
          ],
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            context.read(cartProvider.notifier).addProduct(
              Product('Item ${context.read(cartProvider).length + 1}', 20.0),
            );
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class ProductList extends ConsumerWidget {
  @override
  Widget build(BuildContext context, ScopedReader watch) {
    final cart = watch(cartProvider);
    return ListView.builder(
      itemCount: cart.length,
      itemBuilder: (context, index) {
        return ListTile(
          title: Text(cart[index].name),
          trailing: Text('\$${cart[index].price}'),
          onTap: () {
            context.read(cartProvider.notifier).removeProduct(cart[index]);
          },
        );
      },
    );
  }
}

class CartTotal extends ConsumerWidget {
  @override
  Widget build(BuildContext context, ScopedReader watch) {
    final total = watch(cartProvider.notifier).total;
    return Container(
      padding: EdgeInsets.all(8.0),
      child: Text('Total: \$${total}', style: TextStyle(fontSize: 24)),
    );
  }
}
```
