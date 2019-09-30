# 스플래시 만들기

_작성자 : gmlwo530_

state에 대한 이해도가 있으면 만들 수 있다.

```dart
import 'dart:async';

import 'package:flutter/widgets.dart';

class Splash extends StatefulWidget { // Splash는 Route정의 시 '/'로 정의 하였다. 그러므로 앱이 시작할 때 바로 이 화면으로 시작한다.
  @override
  _SplashState createState() => new _SplashState();
}

class _SplashState extends State<Splash>{
  startTime() async{
    var _duration = new Duration(seconds: 2);
    return new Timer(_duration, navigationPage);
  }

  //2초 후 넘어갈 화면으로 이동시키는 함수이다.
  void navigationPage() {
    Navigator.of(context).pushReplacementNamed('/Home');
  }

  @override
  void initState() {
    // widget이 만들어지고 첫 번째로 호출되는 함수이다.
    super.initState();
    startTime();
  }

  @override
  Widget build(BuildContext context) {
    // 스플래시 이미지를 여기에 추가 시키면 된다.
    return Container(
      constraints: BoxConstraints(
        minHeight: 200.0
      ),
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: <Widget>[
          Text("Splash Image")
        ],
      ),
    );
  }
}
```

---

**Reference**

- [https://medium.com/@vignesh_prakash/flutter-splash-screen-84fb0307ac55](https://medium.com/@vignesh_prakash/flutter-splash-screen-84fb0307ac55)
