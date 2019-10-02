# 네비게이션 (4-1)

작성자 : gmlwo530

## Pass arguments to a named route

- [네비게이션(2)](<https://github.com/today-we-learned-korea/flutter/blob/master/%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%EC%85%98(2)-Navigated%20with%20named%20rotues_gmlwo530.md>) 글에서 특정 식별자(`/user`와 같은)를 통해서 Navigate 하는 방법을 배웠다. 이 방법과 동시 data를 화면에 넘겨 주는 방법을 알아보겠다.

- `ModalRoute.of` 메소드와 `onGenerateRoute()` 함수를 통해서 예제를 진행한다.

- 2가지 방법이 소개 되어 (4-1)과 [(4-2)]()로 나누었다.

### 1. Define the arguments you need to pass

넘겨줄 arguments를 정의하자

```dart
class ScreenArguments {
  final String title;
  final String message;

  ScreenArguments(this.title, this.message);
}
```

### 2. Create a widget that extracts the arguments

그 다음으로 `ScreenArguments`으로부터 `title`와 `message`를 뽑아내서 보여주는 Widget을 만들자.
`ScreenArguments`에 접근하기 위해서 `ModalRoute.of()` 메서드를 이 Widget에서 사용한다.
이 메서드는 현재 route의 `arguments`를 반환한다.

```dart
class ExtractArgumentsScreen extends StatelessWidget {
  static const routeName = '/extractArguments';

  @override
  Widget build(BuildContext context) {
    final ScreenArguments args = ModalRoute.of(context).settings.arguments;

    return Scaffold(
      appBar: AppBar(
        title: Text(args.title),
      ),
      body: Center(
        child: Text(args.message),
      ),
    );
  }
}
```

### 3. Register the widget in the routes table

`MaterialApp`의 routes를 수정합니다.

```dart
  MaterialApp(
    routes : {
      ExtractArgumentsScreen.routeName = (context) => ExtractArgumentsScreen(),
    },
    ...
  )
```

### 4. Navigate to the Widget

`Navigator.pushNamed()`의 arguments 속성에 `ScreenArgument`를 넣어줍니다

```dart
RaisedButton(
  child : Text("Navigate to screen that extracts arguments"),
  onPressed : () {
    Navigator.pushNamed(
      context,
      ExtractArgumentsScreen.routeName,
      arguments: ScreenArguments(
        'Extract Arguments Screen',
        'This message is extracted in the build method.',
      ),
    );
  },
)
```

### 5. Complete Code

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Navigation with Arguments',
      home: HomeScreen(),
      routes: {
        ExtractArgumentsScreen.routeName = (context) => ExtractArgumentsScreen(),
      }
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
              child: Text("Navigate to screen that extracts arguments"),
              onPressed: () {
                Navigator.pushNamed(
                  context,
                  ExtractArgumentsScreen.routeName,
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

class ExtractArgumentsScreen extends StatelessWidget {
  static const routeName = '/extractArguments';

  @override
  Widget build(BuildContext context) {
    final ScreenArguments args = ModalRoute.of(context).settings.arguments;

    return Scaffold(
      appBar: AppBar(
        title: Text(args.title),
      ),
      body: Center(
        child: Text(args.message),
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
