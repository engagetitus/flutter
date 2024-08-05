
---

### Module 6: GetX

#### Lesson 1: Introduction to GetX


# Module 6: GetX

## Lesson 1: Introduction to GetX

### What is GetX?
GetX is an extra-light and powerful state management solution for Flutter. It provides high-performance state management, intelligent dependency injection, and route management.

### Benefits of Using GetX
- High performance and low memory consumption
- Easy and powerful dependency management
- Simplified routing and navigation
- Reactive programming support

### Setting Up GetX
Add the get dependency to your `pubspec.yaml` file:
```yaml
dependencies:
  get: ^4.0.0
```
Basic Example
dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';

class CounterController extends GetxController {
  var count = 0.obs;

  void increment() {
    count++;
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('GetX Example')),
        body: Center(
          child: Obx(() {
            return Text('Count: ${Get.find<CounterController>().count}');
          }),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Get.find<CounterController>().increment();
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Get.put(CounterController());
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('GetX Example')),
        body: Center(
          child: Obx(() {
            return Text('Count: ${Get.find<CounterController>().count}');
          }),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Get.find<CounterController>().increment();
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
Practical Example: Shopping Cart
dart

import 'package:flutter/material.dart';
import 'package:get/get.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Cart Controller
class CartController extends GetxController {
  var products = <Product>[].obs;

  void addProduct(Product product) {
    products.add(product);
  }

  void removeProduct(Product product) {
    products.remove(product);
  }

  double get total {
    return products.fold(0, (sum, item) => sum + item.price);
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Get.put(CartController());
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('GetX Cart Example')),
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
            Get.find<CartController>().addProduct(
              Product('Item ${Get.find<CartController>().products.length + 1}', 20.0),
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
    return Obx(() {
      final cart = Get.find<CartController>().products;
      return ListView.builder(
        itemCount: cart.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(cart[index].name),
            trailing: Text('\$${cart[index].price}'),
            onTap: () {
              Get.find<CartController>().removeProduct(cart[index]);
            },
          );
        },
      );
    });
  }
}

class CartTotal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(8.0),
      child: Obx(() {
        return Text('Total: \$${Get.find<CartController>().total}', style: TextStyle(fontSize: 24));
      }),
    );
  }
}