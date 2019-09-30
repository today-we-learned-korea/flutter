# 네비게이션 (1)

작성자 : gmlwo530

## Navigate to a new screen and back

- Flutter에서는 모든 화면과 페이지를 *routes*라고 부른다. 즉, AOS에서는 Activity, iOS에서는 ViewController와 같다고 보면 된다.

- Flutter에서 route는 `Widget`이다.

- 다음과 같이 두 화면을 이동할 수 있다.
  1. `Navigator.push()` -> 두 번째 route로 이동한다.
  2. `Navigator.pop()` -> 첫 번째 route로 돌아온다.

완성 된 코드에 번호 주석을 달았다. 전체 코드를 우선 보고, 번호가 달린 코드를 살펴보겠다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    title: 'Navigation Basics',
    home: FirstRoute(),
  ));
}

class FirstRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('First Route'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Open route'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondRoute()), // (1)
            );
          },
        ),
      ),
    );
  }
}

class SecondRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Second Route"),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            Navigator.pop(context); //(2)
          },
          child: Text('Go back!'),
        ),
      ),
    );
  }
}
```

(1) `push()`메소드는 Navigator가 관리하는 routes 스택에 `Route`를 추가한다. 이 코드에서는 [MaterialPageRoute](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)를 사용한다. Material이므로 Android 플랫폼의 화면 이동 애니메이션을 가지고 있다.

(2) `pop()`메소드는 Navigator가 관리하는 routes 스택에서 현재 `Route`를 지운다.

---

**Reference**

- [https://flutter.dev/docs/cookbook/navigation/navigation-basics](https://flutter.dev/docs/cookbook/navigation/navigation-basics)
