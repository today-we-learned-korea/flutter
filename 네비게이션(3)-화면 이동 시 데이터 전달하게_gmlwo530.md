# 네비게이션 (3)

작성자 : gmlwo530

## Send data to a new screen

예제를 따라 가보겠다.

### 1. Define a todo class

우선 모델을 정의 하자

```dart
class Todo {
  final String title;
  final String description;

  Todo(this.title, this.description);
}
```

### 2. Create a list of todos

첫 번째 화면에서는 ListView를 통해서 20개의 Todo를 보여주자

```dart
final todos = List<Todo>.generate(
  20,
  (i) => Todo(
        'Todo $i',
        'A description of what needs to be done for Todo $i',
      ),
);
```

### 3. Create a detail screen to display information about a todo

두 번째 화면에서는 todo의 title과 description을 보여주는 화면을 만들자

```dart
class DetailScreen extends StatelessWidget {
  final Todo todo;

  // todo 모델은 무조건 넘어와야 한다.
  DetailScreen({Key key, @required this.todo}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(todo.title),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Text(todo.description),
      ),
    );
  }
}
```

### 4. Complete Code

```dart
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

class Todo {
  final String title;
  final String description;

  Todo(this.title, this.description);
}

void main() {
  runApp(MaterialApp(
    title: 'Passing Data',
    home: TodosScreen(
      todos: List.generate(
        20,
        (i) => Todo(
              'Todo $i',
              'A description of what needs to be done for Todo $i',
            ),
      ),
    ),
  ));
}

class TodosScreen extends StatelessWidget {
  final List<Todo> todos;

  TodosScreen({Key key, @required this.todos}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todos'),
      ),
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(todos[index].title),
            onTap: () {
              // DetailScreen에 constructor를 정의 해주었으므로, 다음과 같이 표현 할 수 있다.
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => DetailScreen(todo: todos[index]),
                ),
              );
            },
          );
        },
      ),
    );
  }
}

class DetailScreen extends StatelessWidget {
  final Todo todo;

  DetailScreen({Key key, @required this.todo}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(todo.title),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Text(todo.description),
      ),
    );
  }
}
```

---

**Reference**

- [https://flutter.dev/docs/cookbook/navigation/named-routes](https://flutter.dev/docs/cookbook/navigation/named-routes)
