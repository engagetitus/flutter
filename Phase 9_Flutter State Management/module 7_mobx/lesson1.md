
---

### Module 7: MobX

#### Lesson 1: Introduction to MobX


# Module 7: MobX

## Lesson 1: Introduction to MobX

### What is MobX?
MobX is a state management library that makes state observable and reacts to changes automatically. It integrates well with Flutter and simplifies the state management process.

### Benefits of Using MobX
- Simple and intuitive state management
- Automatic reactions to state changes
- Supports complex state management scenarios
- Easy integration with Flutter

### Setting Up MobX
Add the mobx and flutter_mobx dependencies to your `pubspec.yaml` file:
```yaml
dependencies:
  mobx: ^2.0.0
  flutter_mobx: ^2.0.0
```
Also, add the mobx_codegen and build_runner dependencies for code generation:

yaml

dev_dependencies:
  mobx_codegen: ^2.0.0
  build_runner: ^2.0.0
Basic Example
dart

import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:mobx/mobx.dart';

// Include generated file
part 'counter.g.dart';

// This is the class used by rest of your codebase
class Counter = _Counter with _$Counter;

// The store-class
abstract class _Counter with Store {
  @observable
  int count = 0;

  @action
  void increment() {
    count++;
  }
}

void main() {
  final counter = Counter();
  runApp(MyApp(counter: counter));
}

class MyApp extends StatelessWidget {
  final Counter counter;

  MyApp({required this.counter});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('MobX Example')),
        body: Center(
          child: Observer(
            builder: (_) => Text('Count: ${counter.count}'),
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: counter.increment,
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
Practical Example: Shopping Cart
dart

import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:mobx/mobx.dart';

// Include generated file
part 'cart.g.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Cart Store
class Cart = _Cart with _$Cart;

abstract class _Cart with Store {
  @observable
  ObservableList<Product> products = ObservableList<Product>();

  @action
  void addProduct(Product product) {
    products.add(product);
  }

  @action
  void removeProduct(Product product) {
    products.remove(product);
  }

  @computed
  double get total {
    return products.fold(0, (sum, item) => sum + item.price);
  }
}

void main() {
  final cart = Cart();
  runApp(MyApp(cart: cart));
}

class MyApp extends StatelessWidget {
  final Cart cart;

  MyApp({required this.cart});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('MobX Cart Example')),
        body: Column(
          children: [
            Expanded(
              child: ProductList(cart: cart),
            ),
            CartTotal(cart: cart),
          ],
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            cart.addProduct(
              Product('Item ${cart.products.length + 1}', 20.0),
            );
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class ProductList extends StatelessWidget {
  final Cart cart;

  ProductList({required this.cart});

  @override
  Widget build(BuildContext context) {
    return Observer(
      builder: (_) {
        return ListView.builder(
          itemCount: cart.products.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(cart.products[index].name),
              trailing: Text('\$${cart.products[index].price}'),
              onTap: () {
                cart.removeProduct(cart.products[index]);
              },
            );
          },
        );
      },
    );
  }
}

class CartTotal extends StatelessWidget {
  final Cart cart;

  CartTotal({required this.cart});

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(8.0),
      child: Observer(
        builder: (_) {
          return Text('Total: \$${cart.total}', style: TextStyle(fontSize: 24));
        },
      ),
    );
  }
}