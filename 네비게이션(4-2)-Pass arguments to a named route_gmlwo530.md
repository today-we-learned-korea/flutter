# 네비게이션 (4-2)

작성자 : gmlwo530

## Pass arguments to a named route

- 2가지 방법이 소개 되어 [(4-1)](<https://github.com/today-we-learned-korea/flutter/blob/master/%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%EC%85%98(4-2)-Pass%20arguments%20to%20a%20named%20route_gmlwo530.md>)과 (4-2)로 나누었다.

- `onGenerateRoute()` 함수를 통해서 예제를 진행한다.

### 1. Define the arguments you need to pass

넘겨줄 arguments를 정의하자

```dart
class ScreenArguments {
  final String title;
  final String message;

  ScreenArguments(this.title, this.message);
}
```

### 2. Create a widget

그 다음으로 `ScreenArguments`으로부터 `title`와 `message`를 뽑아내서 보여주는 Widget을 만들자.
이 Widget은 `ModalRoute`에서 arguments를 받지 않는다.

`MaterialApp`의 속성인 `onGenerateRoute` 함수로 부터 받아서 constructor parameter로써 arguments를 받는다.

```dart
class PassArgumentsScreen extends StatelessWidget {
  static const routeName = '/passArguments';

  final String title;
  final String message;

  const PassArgumentsScreen({
    Key key,
    @required this.title,
    @required this.message,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Text(message),
      ),
    );
  }
}
```

### 3. Register the widget in the routes table

`MaterialApp`의 `onGenerateRoute`를 수정합니다.

```dart
  MaterialApp(
    onGenerateRoute: (settings) {
        if (settings.name == PassArgumentsScreen.routeName) {
          // Cast the arguments to the correct type: ScreenArguments.
          final ScreenArguments args = settings.arguments;

          return MaterialPageRoute(
            builder: (context) {
              return PassArgumentsScreen(
                title: args.title,
                message: args.message,
              );
            },
          );
        }
      },
    ...
  )
```

### 4. Complete Code

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      onGenerateRoute: (settings) {
        if (settings.name == PassArgumentsScreen.routeName) {
          final ScreenArguments args = settings.arguments;

          return MaterialPageRoute(
            builder: (context) {
              return PassArgumentsScreen(
                title: args.title,
                message: args.message,
              );
            },
          );
        }
      },
      title: 'Navigation with Arguments',
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
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            RaisedButton(
              child: Text("Navigate to a named that accepts arguments"),
              onPressed: () {
                Navigator.pushNamed(
                  context,
                  PassArgumentsScreen.routeName,
                  arguments: ScreenArguments(
                    'Extract Arguments Screen',
                    'This message is extracted in the build method.',
                  ),
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}

class PassArgumentsScreen extends StatelessWidget {
  static const routeName = '/passArguments';

  final String title;
  final String message;

  const PassArgumentsScreen({
    Key key,
    @required this.title,
    @required this.message,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Text(message),
      ),
    );
  }
}

class ScreenArguments {
  final String title;
  final String message;

  ScreenArguments(this.title, this.message);
}
```

---

**Reference**

- [https://flutter.dev/docs/cookbook/navigation/navigate-with-arguments](https://flutter.dev/docs/cookbook/navigation/navigate-with-arguments)
