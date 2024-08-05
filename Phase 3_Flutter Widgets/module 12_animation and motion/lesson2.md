Lesson 2: Hero Animation
Overview: Creating hero animations between screens and customizing transitions.

Key Concepts:

Basic Usage of Hero ✈️
Customizing Hero Transitions 🎭
Basic Usage of Hero ✈️

Creating a simple Hero animation:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hero Animation Example'),
        ),
        body: HeroExampleScreen(),
      ),
    );
  }
}

class HeroExampleScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: GestureDetector(
        child: Hero(
          tag: 'hero-1',
          child: FlutterLogo(size: 100),
        ),
        onTap: () {
          Navigator.push(context, MaterialPageRoute(builder: (_) {
            return HeroDetailScreen();
          }));
        },
      ),
    );
  }
}

class HeroDetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Hero Detail Screen'),
      ),
      body: Center(
        child: Hero(
          tag: 'hero-1',
          child: FlutterLogo(size: 200),
        ),
      ),
    );
  }
}
Customizing Hero Transitions 🎭

Customizing the Hero animation:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Hero Animation Example'),
        ),
        body: CustomHeroExampleScreen(),
      ),
    );
  }
}

class CustomHeroExampleScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: GestureDetector(
        child: Hero(
          tag: 'hero-2',
          transitionOnUserGestures: true,
          flightShuttleBuilder: (BuildContext flightContext, Animation<double> animation,
              HeroFlightDirection flightDirection, BuildContext fromHeroContext, BuildContext toHeroContext) {
            return ScaleTransition(
              scale: animation.drive(
                Tween<double>(begin: 0.0, end: 1.0).chain(
                  CurveTween(curve: Curves.fastOutSlowIn),
                ),
              ),
              child: toHeroContext.widget,
            );
          },
          child: FlutterLogo(size: 100),
        ),
        onTap: () {
          Navigator.push(context, MaterialPageRoute(builder: (_) {
            return CustomHeroDetailScreen();
          }));
        },
      ),
    );
  }
}

class CustomHeroDetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Hero Detail Screen'),
      ),
      body: Center(
        child: Hero(
          tag: 'hero-2',
          transitionOnUserGestures: true,
          flightShuttleBuilder: (BuildContext flightContext, Animation<double> animation,
              HeroFlightDirection flightDirection, BuildContext fromHeroContext, BuildContext toHeroContext) {
            return ScaleTransition(
              scale: animation.drive(
                Tween<double>(begin: 0.0, end: 1.0).chain(
                  CurveTween(curve: Curves.fastOutSlowIn),
                ),
              ),
              child: toHeroContext.widget,
            );
          },
          child: FlutterLogo(size: 200),
        ),
      ),
    );
  }
}