
---

### Module 4: Redux

#### Lesson 1: Introduction to Redux


# Module 4: Redux

## Lesson 1: Introduction to Redux

### What is Redux?
Redux is a predictable state container for JavaScript apps, but it can also be used with Dart and Flutter. It helps you write applications that behave consistently, run in different environments, and are easy to test.

### Benefits of Using Redux
- Predictable state updates
- Centralized state management
- Middleware support for asynchronous logic
- Time-travel debugging

### Setting Up Redux
Add the redux and flutter_redux dependencies to your `pubspec.yaml` file:
```yaml
dependencies:
  redux: ^4.0.0
  flutter_redux: ^0.8.0
Basic Example
dart

import 'package:flutter/material.dart';
import 'package:flutter_redux/flutter_redux.dart';
import 'package:redux/redux.dart';

// Actions
class IncrementAction {}

// Reducer
int counterReducer(int state, dynamic action) {
  if (action is IncrementAction) {
    return state + 1;
  }
  return state;
}

void main() {
  final store = Store<int>(counterReducer, initialState: 0);
  runApp(MyApp(store: store));
}

class MyApp extends StatelessWidget {
  final Store<int> store;

  MyApp({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider(
      store: store,
      child: MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('Redux Example')),
          body: Center(
            child: StoreConnector<int, int>(
              converter: (store) => store.state,
              builder: (context, count) {
                return Text('Count: $count');
              },
            ),
          ),
          floatingActionButton: StoreConnector<int, VoidCallback>(
            converter: (store) {
              return () => store.dispatch(IncrementAction());
            },
            builder: (context, callback) {
              return FloatingActionButton(
                onPressed: callback,
                child: Icon(Icons.add),
              );
            },
          ),
        ),
      ),
    );
  }
}
Practical Example: Shopping Cart
dart

import 'package:flutter/material.dart';
import 'package:flutter_redux/flutter_redux.dart';
import 'package:redux/redux.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Actions
class AddProductAction {
  final Product product;
  AddProductAction(this.product);
}

class RemoveProductAction {
  final Product product;
  RemoveProductAction(this.product);
}

// State
class AppState {
  final List<Product> cart;

  AppState(this.cart);

  double get total {
    return cart.fold(0, (sum, item) => sum + item.price);
  }
}

// Reducer
AppState appReducer(AppState state, dynamic action) {
  if (action is AddProductAction) {
    return AppState([...state.cart, action.product]);
  }
  if (action is RemoveProductAction) {
    return AppState(state.cart.where((item) => item != action.product).toList());
  }
  return state;
}

void main() {
  final store = Store<AppState>(
    appReducer,
    initialState: AppState([]),
  );
  runApp(MyApp(store: store));
}

class MyApp extends StatelessWidget {
  final Store<AppState> store;

  MyApp({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider(
      store: store,
      child: MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('Redux Cart Example')),
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
              store.dispatch(AddProductAction(
                Product('Item ${store.state.cart.length + 1}', 20.0),
              ));
            },
            child: Icon(Icons.add),
          ),
        ),
      ),
    );
  }
}

class ProductList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StoreConnector<AppState, List<Product>>(
      converter: (store) => store.state.cart,
      builder: (context, cart) {
        return ListView.builder(
          itemCount: cart.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(cart[index].name),
              trailing: Text('\$${cart[index].price}'),
              onTap: () {
                StoreProvider.of<AppState>(context)
                    .dispatch(RemoveProductAction(cart[index]));
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
      child: StoreConnector<AppState, double>(
        converter: (store) => store.state.total,
        builder: (context, total) {
          return Text('Total: \$${total}', style: TextStyle(fontSize: 24));
        },
      ),
    );
  }
}