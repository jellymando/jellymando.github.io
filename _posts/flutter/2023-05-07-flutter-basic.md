---
title: "Flutter 앱 기본 구조"
categories: [Flutter]
tags: [flutter]
---

{:toc .large-only}

## 앱 구조

```dart
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {};

class MyHomePage extends StatefulWidget {};

class _MyHomePageState extends State<MyHomePage> {};
```

## 앱 실행 부분

```dart
void main() => runApp(MyApp());
```

`main()` 함수는 앱의 시작점이다.

여기서는 runApp 함수에 MyApp 인스턴스를 전달한다.

## StatelessWidget 클래스

```dart
class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp();
    }
}
```

StatelessWidget 클래스는 상태(State)를 가지지 않는 위젯을 구성하는 기본 클래스이다.

이러한 클래스는 프로퍼티 변수를 가지지 않으며 한 번 그려진 후 다시 그리지 않는다.

StatelessWidget 클래스는 `build()` 메서드를 가지고 있으며, 위젯을 생성할 때 호출한다.

## MaterialApp 클래스

```dart
return MaterialApp(
    title: 'Flutter Demo',
    theme: ThemeData(
        primarySwatch: Colors.blue
    ),
    home: MyHomePage(title: 'Flutter Demo Home Page')
);
```

MaterialApp 클래스는 meterial 디자인을 사용한다.

title은 앱의 제목을 나타내며 theme은 테마를 지정한다.

home은 실제로 앱이 표시하는 위젯이다.

## StatefulWidget 클래스

```dart
class MyHomePage extends StatefulWidget {
    MyHomePage({Key key, this.title}) : super(key: key); // 1.

    final String title;

    @override
    _MyHomePageState createState() => _MyHomePageState(); // 2.
}

class _MyHomePageState extends State<MyHomePage> {
    int _counter = 0; // 3.

    @override
    Widget build(BuildContext context) { // 4.
        return Scaffold()
    }
}
```

1. MyHomePage 클래스 생성자는 key와 title 프로퍼티를 받아 super 키워드로 부모 클래스의 생성자에 key를 전달한다.
1. MyHomePage 클래스에는 상속받은 createSate() 메서드를 재정의하여 \_MyHomePageState 클래스의 인스턴스를 반환한다. 이 메서드는 StatefulWidget이 생성될 때 한 번만 실행된다.
1. State 클래스를 상속받은 클래스를 상속 클래스라 한다. 생태 클래스는 변경 가능한 프로퍼티 변수(State)를 가지며 이 변수를 수정하여 화면을 다시 그릴 수 있다.
1. `build()` 메서드를 가지며 상태에 따라 화면에 그려질 코드를 여기에 작성한다.

## 위젯에서 위젯으로 값 전달

```dart
class MyHomePage extends StatefulWidget {
    // 생성자
    MyHomePage({Key key, this.title}) : super(key: key);

    final String title;

    @override
    _MyHomePageState createState() => _MyHomePageState();
}

// 상태 클래스
class _MyHomePageState extends State<MyHomePage> {
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(widget.title)
            )
        );
    }
}
```

MyHomePage 클래스로 전달받은 title 값은 `this.title` 매개변수로 전달되어 필드 상수인 `String title`에 대입된다.

\_MyHomePageState 클래스에서 StatefulWidget의 title에 접근하려면 widget 프로퍼티를 사용하여 `widget.title`로 접근한다.

## 상태 변경

```dart
class _MyHomePageState extends State<MyHomePage> {
    int _counter = 0;

    void _increamentCounter() {
        setState(() {
            _counter++;
        })
    }

    @override
    Widget build(BuildConext context) {
        return Scaffold()
    }
}
```

`setState()` 메서드는 State 클래스가 제공하는 메서드이다.

State 위젯 내부 메서드나 `initState()`, `didUpdateWidget` 등의 생명 주기 메서드에서 실행한다. `build()` 내부에서 호출하는 것은 권장하지 않는다.

`setState()` 메서드로 상태를 변경하면 `build()` 메서드가 다시 실행되어 화면을 다시 그리게 된다.

위 코드에서 변경 가능한 상태는 \_counter 변수이며 이 값이 변경될 때마다 화면을 다시 그리면 동적인 화면을 가진 앱이 된다.

## 함수 실행

Flutter에서 함수를 즉시 실행하려면 StatefulWidget인 경우 `initState()` 메서드 내에서, StatelessWidget인 경우 `build()` 메서드 내에서 호출한다.

### StatefulWidget

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  void initState() {
    super.initState();
    // Call your function here
    myFunction();
  }

  void myFunction() {
    // Function logic goes here
    print('My function is running immediately!');
  }

  @override
  Widget build(BuildContext context) {
    // Build your widget UI here
    return Container();
  }
}
```

### StatelessWidget

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Call your function here
    myFunction();

    // Build your widget UI here
    return Container();
  }

  void myFunction() {
    // Function logic goes here
    print('My function is running immediately!');
  }
}
```
