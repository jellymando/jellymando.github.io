---
title: "[JAVA] 인터페이스와 다형성, 익명/중첩 클래스"
date: 2025-02-23 22:00:00 +0900
categories: [JAVA]
tags: [java]
---

{:toc .large-only}

## 추상 클래스

- 클래스 정의에 `abstract` 키워드를 사용함
- <u>객체 생성을 할 수 없음</u>
  - 구체적이지 못한 불완전한 클래스라는 의미
- 추상 클래스는 자식 클래스로 상속되어 사용함
  - 공통으로 사용할 데이터 필드와 메서드를 추상 클래스에서 정의
  - 자식 클래스에서 추상 메서드를 구현해야 함
  - 자식 클래스가 추상 메서드를 구현하지 않으면 계속해서 자식 클래스도 추상 클래스여야 함
- 일반 클래스와 인터페이스의 중간적 성격을 가짐
- **의미적으로 유사한** 자식 클래스를 묶고자 할 때 추상 클래스를 사용

```java
abstract class Shape {
  ...
}

public class Main {
	public static void main(String args[]) {
	  Shape s = new Shape(); //에러: 추상 클래스로 객체 생성을 할 수 없음
	}
}
```

### 추상 메서드

- 메서드 정의에 `abstract` 키워드를 사용함
- 몸체의 구현 없이 형식만 존재하는 메서드
  - 메서드 이름과 인자, 반환형에 관한 선언만 존재함
  - 자식 클래스에 상속됐을 때 몸체의 구현이 필요함
- 상반된 의미의 `final`과 함께 사용할 수 없음
- 추상 클래스 또는 인터페이스에서 선언되어야 함

```java
abstract class Shape {
	abstract public double getArea();
}
```

## 인터페이스

- 100% 추상적 클래스
  - 참조형이며 직접적 객체 생성은 불가
- 정의할 때 `interface`를 사용
  - 인터페이스의 이름은 보통 형용사임 ex) Runnable, Serializable, Comparable
- 모든 메서드가 추상 메서드(public abstract)
  - 몸체 없이 구현되어야 할 메서드의 형식(반환형, 이름, 매개변수)만 정의해 둠
  - 단, default 인스턴스 메서드와 static 메서드는 몸체를 구현해야 함
  - 인터페이스에서 `abstract` 접근 제어자 생략 가능 (생략하면 기본적으로 public abstract)
- 데이터 필드는 클래스 상수(public static final)만 가능
- 의미적으로는 관련이 없으나 **기능적으로 유사한** 클래스들을 묶을 때 인터페이스를 사용

## 인터페이스의 상속

### 자식 인터페이스에 상속

- 자식 인터페이스가 부모 인터페이스를 상속받는 경우
- `extends` 키워드 사용
- 여러 부모 인터페이스를 상속받는 다중 상속 가능

```java
interface SuperInterface {
  public void func1();
  public void func2();
}

// 자식 인터페이스에 부모 인터페이스 상속
interface SubInterface extends SuperInterface {
  public void func3();
}
```

### 자식 클래스에 상속

- 자식 클래스가 부모 인터페이스를 상속받는 경우
- `implements` 키워드 사용
- 여러 부모 인터페이스를 상속받는 다중 상속 가능
  - 부모 클래스-자식 클래스는 1개만 상속 가능

```java
interface Movable {
  void add(double dx, double dy);
  void sub(double dx, double dy);
}

interface Scalable {
  void mul(double s);
  void div(double s);
}

// 자식 클래스에 부모 인터페이스 다중 상속
class Point implements Movable, Scalable {
  ...
}
```

```java
interface Figure {
  double getArea();
}

class Triangle implements Figure {
  private double height, width;

  public Triangle(double h, double w) {
    height = h;
    width = w;
  }

  // 자식 클래스에서 인터페이스 메서드 몸체 구현
  public double getArea() {
    return height * width * 0.5;
  }
}
```

### 디폴트 메서드

- 인터페이스에서 몸체가 있는 메서드를 선언할 때 사용
- `default` 키워드를 사용하여 선언
- 자식 클래스에서 디폴트 메서드를 구현하지 않고 그대로 사용할 수 있음
- 인터페이스에 새 메서드를 추가할 때 기존 자식 클래스들의 코드 수정을 피하기 위함
  - 만약 추상 메서드를 추가한다면 자식 클래스들도 추가된 메서드의 몸체를 구현하도록 수정해야 함

```java
interface DoIt {
  void doSomething();
  int doSomethingElse(String s);

  default boolean didItWork(int i, String s) {
    ...
  }
}
```

## 다형성

- 한 부모에서 나온 두 자식 객체는 비슷하지만 다른 다양한 형상을 가진다.
- 하나의 클래스에서 오버로딩된 메서드들은 유사하지만 조금씩 다른 기능을 수행함

### 형변환

- 상속 관계에 따라 상위/하위 자료형 관계가 설정됨
- 상속 관계에 있는 클래스 간에는 타입 변환이 가능함
  - 자식(하위) 클래스에서 부모(상위) 클래스로의 자동 형변환 가능 (업캐스팅)
- 상위 유형의 변수는 하위 객체를 참조할 수 있음
  - ex) `Animal animal = new Dog(); //하위 객체 참조`
- 컴파일할 때는 객체의 필드나 메서드가 선언 유형에 정의되어 있는지 확인함
- 변수의 선언 유형이 아닌 실제 유형에 따라 수행되는 메서드가 결정됨 (동적 바인딩)
- 코드의 유연성과 재사용성을 높이며, 동적 바인딩을 통해 실제 유형을 명시적으로 다룰 필요가 없어짐

```java
class A {
  public void func() {
    System.out.println("A");
  }
}

class B extends A {
  public void func() {
    System.out.println("B");
  }
}

class C extends B {
  public void func() {
    System.out.println("C");
  }
  public void func2() {
    System.out.println("C2");
  }
}

public class Main {
  public static void main(String args[]) {
    A a = new B();
    a.func(); // B
    a = new C();
    a.func(); // C
    a.func2(); // 컴파일 에러: The method func2() is undefined for the type A
  }
}
```

## 열거형

- 미리 정의된 상수값의 집합을 만들기 위한 자료형
- `enum`을 사용하여 정의
- 열거형으로 선언된 변수에는 미리 지정된 값만 대입 가능
- 상수값을 배열로 리턴하는 static 메서드인 `values()` 제공

```java
enum Day {
  SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}

public class Main {
  public static void main(String args[]) {
    Day day = Day.MONDAY;
    for (Day d: Day.values()) // 열거형 상수값을 배열로 리턴
      System.out.println(d);
    ...
  }
}
```

### 열거형 정의

- 열거형 정의에 데이터 필드와 메서드를 포함할 수 있음
  - 상수 선언이 데이터 필드나 메서드보다 먼저 정의되어야 하며, 세미콜론(;)으로 끝나야 함
- 열거형에서 상수값은 마치 하나의 객체와 같음
  - `열거형이름.상수값` 형식 사용
  - `열거형이름.상수값`은 그 자체가 열거형의 인스턴스
- 생성자를 가질 수 있음
  - 생성자는 열거형과 같은 이름을 가지며 접근 제어자는 생략 또는 private이어야 함
  - 열거형 상수(객체)에 대한 초기화를 수행함
  - 생성자는 상수가 사용될 때 한꺼번에 자동 호출됨

```java
enum BaseballTeam {
  LG(40, 30), SS(30, 40), KT(20, 50), SK(35, 35), NC(55, 15);

  private final int win;
  private final int lose;

  private BaseballTeam(int win, int lose) {
    this.win = win;
    this.lose = lose;
  }

  public double winsRate() {
    return (win * 100.0) / (win + lose);
  }
}

public class Main {
  public static void main(String args[]) {
    BaseballTeam bt = BaseballTeam.LG; // BaseballTeam의 모든 상수(LG, SS, KT..)의 생성자가 한꺼번에 호출됨
    System.out.println(bt.winsRate());
  }
}
```

## 익명 클래스

- 일회성으로 객체를 생성하기 위한 클래스
- 정의와 동시에 객체를 생성할 수 있음
- 부모 클래스를 상속받거나 인터페이스를 구현하도록 익명 클래스를 정의함

```java
class CSuper {
 public int a = 10;
 public void method1() {
  System.out.println("super1");
 }
 public void method2() {
  System.out.println("super2");
 }
}

public class Main {
  public static void main(String args[]) {
    CSuper sub = new CSuper() { // 익명 자식 클래스
      public int b = 20;
      public void method1() { // 부모 클래스의 메서드 재정의
        System.out.println("sub1");
      }
      public void method3() {
        System.out.println("sub3");
      }
    };

    sub.method1(); // sub1
    sub.method2(); // super2
    sub.method3(); // 컴파일 오류: The method method3() is undefined for the type CSuper
    System.out.println(sub.a); // 10
    System.out.println(sub.b); // 컴파일 오류: b cannot be resolved or is not a field
  }
}
```

## 중첩 클래스

- 클래스 내부에 또 다른 클래스를 정의하는 것
- 외부(outer) 클래스, 내부(inner) 클래스라고도 하며 내부 클래스가 외부 클래스의 멤버가 됨
- 내부 클래스는 일반 클래스와 다르게 private, protected 접근 제어자 사용 가능
- 일반적으로 내부 클래스는 외부 클래스의 필드와 관련된 작업을 처리

### static 중첩 클래스

- 외부 클래스의 객체 생성과 무관하게 사용 가능
- 외부 클래스의 정적 멤버에 접근 가능

### non-static 중첩 클래스

- 외부 클래스의 객체가 생성된 이후 사용 가능
- 객체 생성 방법은 `외부클래스.new 내부클래스()`
- 메서드는 this 외에 외부 클래스 객체의 참조(외부클래스.this)를 가지고 있음
- 외부 클래스의 모든 멤버에 접근 가능

```java
class OuterClass {
  public int x = 0;

  class InnerClass {
    public int x = 1;

    void methodInnerClass() {
      System.out.println("this.x = " + this.x + ", OuterClass.this.x = " + OuterClass.this.x);
    }
  }
}

public class Main {
  public static void main(String args[]) {
    OuterClass oc = new OuterClass();
    OuterClass.InnerClass ic = oc.new InnerClass();
    ic.methodInnerClass(); // this.x = 1, OuterClass.this.x = 0
  }
}
```
