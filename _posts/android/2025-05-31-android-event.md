---
title: "[Android] 이벤트 처리"
categories: [Android]
tags: [android]
---

{:toc .large-only}

## 이벤트 핸들러

- 안드로이드 프레임워크에서 사용자의 터치 반응이나 시스템 구성요소에서 발생되는 이벤트를 처리하는 주체
- 특정 이벤트가 발생할 때 이벤트의 발생을 탐지하고 이벤트에 대응하는 기능을 실행시킴

### 콜백 메소드

- 특정 이벤트가 발생했을 때 안드로이드 프레임워크에 의해 자동으로 호출되는 메소드
- 클래스의 추상 메소드를 개발자의 의도에 맞게 구현하여 이벤트 발생 시점에 콜백 메소드를 실행시킴

### View를 통한 콜백 메소드의 구현

- View를 상속받아 View 클래스의 추상 메소드를 재정의(오버라이드)하여 콜백 메소드를 구현함

| 콜백 메소드                                                      | 설명                                |
| ---------------------------------------------------------------- | ----------------------------------- |
| boolean onTouchEvent(MotionEvent event)                          | 화면을 터치했을 때 호출             |
| boolean onKeyDown(int keyCode, KeyEvent event)                   | 키를 눌렀을 때 호출                 |
| boolean onKeyUp(int keyCode, KeyEvent event)                     | 키를 누른 상태에서 뗄 때 호출       |
| boolean onTrackballEvent(MotionEvent event)                      | 트랙볼이 사용될 때 호출             |
| boolean onFocusChanged(boolean hasFocused, int dir, Rect Rected) | View가 포커스를 얻거나 잃을 때 호출 |

```java
class MyView extends View {
  public MyView(Context context) {
    super(context);
  }

  // View에 터치 이벤트가 발생할 때마다 호출되는 콜백 메소드
  // 매개변수로 터치 이벤트의 종류와 좌표 정보를 가진 MotionEvent 객체를 받음
  public boolean onTouchEvent(MotionEvent event) {
    super.onTouchEvent(event);
    if (event.getAction() == MotionEvent.ACTION_DOWN) {
      Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
      return true;
    }
    return false;
  }
}
```

### 이벤트 리스너

- View 내부의 특정 이벤트를 처리하는 인터페이스
- 특정 이벤트가 발생하는 시점까지 대기하고 있다가 발생된 이벤트에 부합되는 콜백 메소드를 수행함
- 콜백 메소드는 하나의 이벤트만 처리하지만 이벤트 리스너는 여러 이벤트를 등록하여 처리할 수 있음
- 이벤트 리스너 인터페이스는 이벤트 리스너가 동작하기 위한 틀만 제공하며, 이벤트를 처리하는 메소드를 구현해야 함

### 클래스를 통한 이벤트 리스너의 구현

- 클래스 선언문에서 이벤트 리스너 인터페이스를 상속받고 클래스 내부에 이벤트 핸들러 메소드를 구현함
- 모든 이벤트에 대해 클래스를 만든다면 코드의 양이 많아지고 복잡해짐

| 이벤트 리스너              | 콜백 메소드                                        | 설명                                          |
| -------------------------- | -------------------------------------------------- | --------------------------------------------- |
| View.onTouchListener       | boolean onTouch(View v, MotionEvent event)         | View를 터치했을 때 호출                       |
| View.onKeyListener         | boolean onKey(View v, int keyCode, KeyEvent event) | 키를 누르거나 뗄 때 호출                      |
| View.onClickListener       | boolean onClick(View v)                            | View를 클릭할 때 호출                         |
| View.onLongClickListener   | boolean onLongClick(View v)                        | View를 길게 클릭할 때 호출                    |
| View.onFocusChangeListener | boolean onFocusChange(View v, boolean hasFocused)  | 포커스가 한 View에서 다른 View로 바뀔 때 호출 |
| View.onDragListener        | boolean onDarg(View v, DragEvent event)            | View를 드래그할 때 호출                       |

```java
public class MainActivity extends Activity {
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    View vw = new View(this);
    vw.setOnTouchListener(TouchListener); // View에 이벤트 리스너 등록
    setContentView(vw);
  }

  // 클래스 선언문에서 이벤트 리스너 인터페이스를 상속받음
  class TouchListenerClass implements View.onTouchListener {
    public boolean onTouch(View v, MotionEvent event) {
      if (event.getAction() == MotionEvent.ACTION_DOWN) {
        Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
        return true;
      }
      return false;
    }
  }
  TouchListenerClass TouchListener = new TouchListenerClass();
}
```

### 액티비티를 통한 이벤트 리스너의 구현

- 액티비티 선언문에서 이벤트 리스너 인터페이스를 상속받고 액티비티 내부에 이벤트 핸들러 메소드를 구현함
- 별도의 이벤트 리스너 클래스를 선언할 필요가 없어 코드가 간결해짐

```java
// 액티비티 선언문에서 이벤트 리스너 인터페이스를 상속받음
public class MainActivity extends Activity implements View.onTouchListener {
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    View vw = new View(this);
    vw.setOnTouchListener(this);  // View에 이벤트 리스너 등록
    setContentView(vw);
  }

  // onTouch 메소드를 재정의함
  public boolean onTouch(View v, MotionEvent event) {
    if (event.getAction() == MotionEvent.ACTION_DOWN) {
      Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
      return true;
    }
    return false;
  }
}
```

### View를 통한 이벤트 리스너의 구현

- View 클래스 선언문에서 이벤트 리스너 인터페이스를 상속받음
- 액티비티에서 직접 이벤트 리스너를 구현하는 것이 아니라 클래스에서 View를 상속받아 이벤트 리스너를 구현하므로 액티비티에 종속적이지 않아 클래스 재사용 면에서 유리함

```java
public class MainActivity extends Activity {
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    View vw = new View(this);
    vw.setOnTouchListener(this);  // View에 이벤트 리스너 등록
    setContentView(vw);
  }

  // 클래스 선언문에서 이벤트 리스너 인터페이스를 상속받음
  class MyView extends View implements View.onTouchListener {
    public MyView(Context context) {
      super(context);
    }

    public boolean onTouch(View v, MotionEvent event) {
      if (event.getAction() == MotionEvent.ACTION_DOWN) {
        Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
        return true;
      }
      return false;
    }
  }
}
```

## 이벤트 핸들러 우선순위

1. View의 인터페이스 리스너
1. View의 콜백 메소드
1. 액티비티의 콜백 메소드

- 이벤트 중첩에서 안쪽일수록 우선순위가 높음
- 각 이벤트 핸들러의 반환값에 따라 다음 순위의 이벤트 핸들러에 대한 호출 여부를 결정함
  - true를 반환하면 더 이상 이벤트를 전달하지 않고 처리가 종료되고, false를 반환하면 다음 순위의 이벤트 핸들러 메소드가 호출됨

```java
public class MainActivity extends Activity {
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    View vw = new View(this);

    // 1. View의 이벤트 리스너에서 처리
    vw.setOnTouchListener(new View.onTouchListener() {
      public boolean onTouch(View v, MotionEvent event) {
        if (event.getAction() == MotionEvent.ACTION_DOWN) {
          Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
          return true;
        }
        return false;
      }
    });
    setContentView(vw);
  }

  // 2. View의 onTouchEvent() 콜백 메소드에서 처리
  class MyView extends View {
    public MyView(Context context) {
      super(context);
    }

    public boolean onTouchEvent(MotionEvent event) {
      super.onTouchEvent(event);
      if (event.getAction() == MotionEvent.ACTION_DOWN) {
        Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
        return true;
      }
      return false;
    }
  }

  // 3. 액티비티의 onTouchEvent() 콜백 메소드에서 처리
  public boolean onTouchEvent(MotionEvent event) {
    if (event.getAction() == MotionEvent.ACTION_DOWN) {
      Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
      return true;
    }
    return false;
  }
}
```
