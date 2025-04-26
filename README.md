## 🎨 1. Custom Theme

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

final ThemeData customTheme = ThemeData(
  primaryColor: Colors.deepPurple,
  colorScheme: ColorScheme.fromSwatch().copyWith(secondary: Colors.teal),
  scaffoldBackgroundColor: Colors.white,
  textTheme: TextTheme(
    headline1: TextStyle(fontSize: 32, fontWeight: FontWeight.bold),
    bodyText1: TextStyle(fontSize: 16, color: Colors.black87),
  ),
);

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: customTheme,
      home: Scaffold(
        appBar: AppBar(title: Text("Custom Theme")),
        body: Center(child: Text("Hello Themed World", style: Theme.of(context).textTheme.bodyText1)),
      ),
    );
  }
}
```

---

## 🧩 2. AnimatedContainer

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool _big = false;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("AnimatedContainer")),
        body: Center(
          child: GestureDetector(
            onTap: () => setState(() => _big = !_big),
            child: AnimatedContainer(
              duration: Duration(seconds: 1),
              width: _big ? 200 : 100,
              height: _big ? 200 : 100,
              color: _big ? Colors.blue : Colors.red,
              curve: Curves.easeInOut,
            ),
          ),
        ),
      ),
    );
  }
}
```

---

## 👆 3. Microinteraction (InkWell)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: InkWell(
            onTap: () {
              print("Tapped!");
            },
            borderRadius: BorderRadius.circular(8),
            child: Container(
              padding: EdgeInsets.all(16),
              decoration: BoxDecoration(
                color: Colors.blue,
                borderRadius: BorderRadius.circular(8),
              ),
              child: Text("Press Me", style: TextStyle(color: Colors.white, fontSize: 18)),
            ),
          ),
        ),
      ),
    );
  }
}
```

---

## 👆 4.AnimationController

```dart
import 'package:flutter/material.dart';

class SimpleAnimation extends StatefulWidget {
  @override
  _SimpleAnimationState createState() => _SimpleAnimationState();
}

class _SimpleAnimationState extends State<SimpleAnimation> 
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _size;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true); // Automatically loops back and forth

    _size = Tween<double>(begin: 100, end: 200).animate(_controller);
  }

  @override
  void dispose() {
    _controller.dispose(); // Prevents memory leaks
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _size,
      builder: (context, _) => Container(
        width: _size.value,
        height: _size.value,
        color: Colors.blue,
      ),
    );
  }
}
```
---

## 🌫️ 5. AnimatedOpacity

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool _visible = true;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("AnimatedOpacity")),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              AnimatedOpacity(
                opacity: _visible ? 1.0 : 0.0,
                duration: Duration(seconds: 1),
                child: Container(
                  width: 200,
                  height: 200,
                  color: Colors.green,
                ),
              ),
              ElevatedButton(
                onPressed: () => setState(() => _visible = !_visible),
                child: Text(_visible ? 'Hide' : 'Show'),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## 🚀 6. Hero Animation

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: FirstScreen()));

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Hero Animation")),
      body: Center(
        child: InkWell(
          onTap: () {
            Navigator.push(context, MaterialPageRoute(builder: (_) => SecondScreen()));
          },
          child: Hero(
            tag: 'imageHero',
            child: Image.network('https://picsum.photos/200', width: 100, height: 100),
          ),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Second Screen")),
      body: Center(
        child: Hero(
          tag: 'imageHero',
          child: Image.network('https://picsum.photos/200', width: 300, height: 300),
        ),
      ),
    );
  }
}
```

---

## 🎞️ 7. Rive Integration

**Note:** Rive needs assets and will only work in a full Flutter project (not online editors).

1. Add to `pubspec.yaml`:
```yaml
dependencies:
  rive: ^0.12.4
```

2. Load a `.riv` file:

```dart
import 'package:flutter/material.dart';
import 'package:rive/rive.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: RiveAnimation.asset(
            'assets/animation.riv',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}
```

---

## ⚙️ 8. Reduced Motion (MediaQuery)

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: ReducedMotionExample());
  }
}

class ReducedMotionExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final reduceMotion = MediaQuery.of(context).disableAnimations;
    return Scaffold(
      appBar: AppBar(title: Text("Reduced Motion: $reduceMotion")),
      body: Center(
        child: Text(
          reduceMotion ? "Animations are off" : "Animations are on",
          style: TextStyle(fontSize: 18),
        ),
      ),
    );
  }
}
```
