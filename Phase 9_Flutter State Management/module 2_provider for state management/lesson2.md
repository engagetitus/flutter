# Lesson 2: Advanced Provider Usage

## MultiProvider

Using `MultiProvider` to provide multiple providers at once:

```dart
void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => Counter()),
        ChangeNotifierProvider(create: (context) => AnotherModel()),
      ],
      child: MyApp(),
    ),
  );
}
```

## ProxyProvider

Creating a provider that depends on other providers:

```dart

void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => Counter()),
        ProxyProvider<Counter, AnotherModel>(
          update: (context, counter, anotherModel) => AnotherModel(counter),
        ),
      ],
      child: MyApp(),
    ),
  );
}
```

## Selector

Optimizing the Consumer widget using Selector:

```dart

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Example')),
        body: Center(
          child: Selector<Counter, int>(
            selector: (context, counter) => counter.count,
            builder: (context, count, child) {
              return Text('Count: $count');
            },
          ),
        ),
      ),
    );
  }
}
```

## Practical Example: Enhanced Shopping Cart

```dart

import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Cart Model
class Cart with ChangeNotifier {
  List<Product> _items = [];

  List<Product> get items => _items;

  void addProduct(Product product) {
    _items.add(product);
    notifyListeners();
  }

  void removeProduct(Product product) {
    _items.remove(product);
    notifyListeners();
  }

  double get total {
    return _items.fold(0, (sum, item) => sum + item.price);
  }
}

void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => Cart()),
        ChangeNotifierProvider(create: (context) => AnotherModel()),
      ],
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Cart Example')),
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
            Provider.of<Cart>(context, listen: false).addProduct(
              Product('Item ${context.read<Cart>().items.length + 1}', 20.0),
            );
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class ProductList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<Cart>(
      builder: (context, cart, child) {
        return ListView.builder(
          itemCount: cart.items.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(cart.items[index].name),
              trailing: Text('\$${cart.items[index].price}'),
              onTap: () {
                cart.removeProduct(cart.items[index]);
              },
            );
          },
        );
      },
    );
  }
}

class CartTotal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(8.0),
      child: Consumer<Cart>(
        builder: (context, cart, child) {
          return Text('Total: \$${cart.total}', style: TextStyle(fontSize: 24));
        },
      ),
    );
  }
}
```
