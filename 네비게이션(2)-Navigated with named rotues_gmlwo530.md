# 네비게이션 (2)

작성자 : gmlwo530

## Navigate with named routes

- 서비스를 만들다 보면 A 화면으로 이동하는 경우가 B 화면, C 화면 등 여러 화면에서 이루어 질 수 있다. 이때 마다 각 화면에 A 화면 Widget을 만들어야 하므로 비효율적이다.

- named routes와 `Navigator.pushNamed()` 함수를 이용하면 이 문제를 해결 할 수 있다.

완성 된 코드에 번호 주석을 달았다. 전체 코드를 우선 보고, 번호가 달린 코드를 살펴보겠다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp( // (1)
    title: 'Named Routes Demo',
    initialRoute: '/',
    routes: {
      '/': (context) => FirstScreen(),
      '/second': (context) => SecondScreen(),
    },
  ));
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('First Screen'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Launch screen'),
          onPressed: () {
            Navigator.pushNamed(context, '/second'); // (2)
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Second Screen"),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('Go back!'),
        ),
      ),
    );
  }
}
```

(1) `MaterialApp`의 추가 속성인 `initialRoute`와 `routes`를 이용하여 routes를 정의해준다. `initialRoute`는 앱이 시작 될때 처음 들어가는 화면을 결정한다.

(2) `Navigator.pushNamed()` 함수를 이용하여 화면을 이동한다.

---

**Reference**

- [https://flutter.dev/docs/cookbook/navigation/named-routes](https://flutter.dev/docs/cookbook/navigation/named-routes)
