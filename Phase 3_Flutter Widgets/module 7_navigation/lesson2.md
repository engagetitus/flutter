
#### Lesson 2: Advanced Navigation Techniques
- **Overview**: Exploring advanced navigation techniques in Flutter.
- **Key Concepts**:
  - Passing Data Between Screens 📤
  - Using Navigator 2.0 🧭


# Passing Data Between Screens 📤
- **Passing data while navigating**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: HomeScreen(),
      );
    }
  }

  class HomeScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Home Screen'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => SecondScreen(data: 'Hello from Home Screen!'),
                ),
              );
            },
            child: Text('Go to Second Screen'),
          ),
        ),
      );
    }
  }

  class SecondScreen extends StatelessWidget {
    final String data;

    SecondScreen({required this.data});

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Second Screen'),
        ),
        body: Center(
          child: Text(data),  // Displaying the passed data
        ),
      );
    }
  }
Using Navigator 2.0 🧭
Implementing Navigator 2.0:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final _routerDelegate = MyRouterDelegate();
  final _routeInformationParser = MyRouteInformationParser();

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routerDelegate: _routerDelegate,
      routeInformationParser: _routeInformationParser,
    );
  }
}

class MyRouterDelegate extends RouterDelegate<MyRoutePath>
    with ChangeNotifier, PopNavigatorRouterDelegateMixin<MyRoutePath> {
  final GlobalKey<NavigatorState> navigatorKey;

  MyRouterDelegate() : navigatorKey = GlobalKey<NavigatorState>();

  MyRoutePath _currentPath = MyRoutePath.home();

  @override
  MyRoutePath get currentConfiguration => _currentPath;

  @override
  Widget build(BuildContext context) {
    return Navigator(
      key: navigatorKey,
      pages: [
        MaterialPage(
          key: ValueKey('HomePage'),
          child: HomePage(),
        ),
        if (_currentPath.isDetailsPage)
          MaterialPage(
            key: ValueKey('DetailsPage'),
            child: DetailsPage(),
          ),
      ],
      onPopPage: (route, result) {
        if (!route.didPop(result)) {
          return false;
        }

        _currentPath = MyRoutePath.home();
        notifyListeners();
        return true;
      },
    );
  }

  @override
  Future<void> setNewRoutePath(MyRoutePath path) async {
    _currentPath = path;
  }
}

class MyRouteInformationParser extends RouteInformationParser<MyRoutePath> {
  @override
  Future<MyRoutePath> parseRouteInformation(
      RouteInformation routeInformation) async {
    final uri = Uri.parse(routeInformation.location!);

    if (uri.pathSegments.isEmpty) {
      return MyRoutePath.home();
    }

    if (uri.pathSegments.length == 2 && uri.pathSegments[0] == 'details') {
      return MyRoutePath.details();
    }

    return MyRoutePath.home();
  }
}

class MyRoutePath {
  final bool isHomePage;
  final bool isDetailsPage;

  MyRoutePath.home()
      : isHomePage = true,
        isDetailsPage = false;

  MyRoutePath.details()
      : isHomePage = false,
        isDetailsPage = true;
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Page'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate to details page
            final delegate =
                Router.of(context).routerDelegate as MyRouterDelegate;
            delegate.setNewRoutePath(MyRoutePath.details());
          },
          child: Text('Go to Details Page'),
        ),
      ),
    );
  }
}

class DetailsPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Details Page'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate back to home page
            final delegate =
                Router.of(context).routerDelegate as MyRouterDelegate;
            delegate.setNewRoutePath(MyRoutePath.home());
          },
          child: Text('Go Back to Home Page'),
        ),
      ),
    );
  }
}