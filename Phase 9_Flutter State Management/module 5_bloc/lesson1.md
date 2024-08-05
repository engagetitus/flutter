
---

### Module 5: Bloc

#### Lesson 1: Introduction to Bloc


# Module 5: Bloc

## Lesson 1: Introduction to Bloc

### What is Bloc?
Bloc (Business Logic Component) is a state management library that helps to separate business logic from UI. It makes it easier to test, reuse, and maintain the code by following the principles of the BLoC pattern.

### Benefits of Using Bloc
- Clear separation of business logic and UI
- Easy to test and maintain
- Built-in support for streams
- Well-defined state transitions

### Setting Up Bloc
Add the bloc and flutter_bloc dependencies to your `pubspec.yaml` file:
```yaml
dependencies:
  bloc: ^8.0.0
  flutter_bloc: ^8.0.0
```
Basic Example
dart

import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

// Event
abstract class CounterEvent {}
class Increment extends CounterEvent {}

// State
class CounterState {
  final int count;
  CounterState(this.count);
}

// Bloc
class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterState(0));

  @override
  Stream<CounterState> mapEventToState(CounterEvent event) async* {
    if (event is Increment) {
      yield CounterState(state.count + 1);
    }
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: BlocProvider(
        create: (context) => CounterBloc(),
        child: CounterPage(),
      ),
    );
  }
}

class CounterPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Bloc Example')),
      body: Center(
        child: BlocBuilder<CounterBloc, CounterState>(
          builder: (context, state) {
            return Text('Count: ${state.count}');
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          context.read<CounterBloc>().add(Increment());
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
Practical Example: Shopping Cart
dart

import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Events
abstract class CartEvent {}
class AddProduct extends CartEvent {
  final Product product;
  AddProduct(this.product);
}
class RemoveProduct extends CartEvent {
  final Product product;
  RemoveProduct(this.product);
}

// State
class CartState {
  final List<Product> products;
  CartState(this.products);

  double get total {
    return products.fold(0, (sum, item) => sum + item.price);
  }
}

// Bloc
class CartBloc extends Bloc<CartEvent, CartState> {
  CartBloc() : super(CartState([]));

  @override
  Stream<CartState> mapEventToState(CartEvent event) async* {
    if (event is AddProduct) {
      yield CartState([...state.products, event.product]);
    }
    if (event is RemoveProduct) {
      yield CartState(state.products.where((item) => item != event.product).toList());
    }
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: BlocProvider(
        create: (context) => CartBloc(),
        child: CartPage(),
      ),
    );
  }
}

class CartPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Bloc Cart Example')),
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
          BlocProvider.of<CartBloc>(context).add(
            AddProduct(Product('Item ${BlocProvider.of<CartBloc>(context).state.products.length + 1}', 20.0)),
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}

class ProductList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<CartBloc, CartState>(
      builder: (context, state) {
        return ListView.builder(
          itemCount: state.products.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(state.products[index].name),
              trailing: Text('\$${state.products[index].price}'),
              onTap: () {
                BlocProvider.of<CartBloc>(context).add(RemoveProduct(state.products[index]));
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
      child: BlocBuilder<CartBloc, CartState>(
        builder: (context, state) {
          return Text('Total: \$${state.total}', style: TextStyle(fontSize: 24));
        },
      ),
    );
  }
}