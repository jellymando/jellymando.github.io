---
title: "C++ 배열, 포인터, 참조"
categories: [C++]
tags: [cpp]
---

{:toc .large-only}

## 배열

동일한 자료형의 값을 여러 개 저장할 수 있는 연속적으로 할당된 공간을 묶어 하나의 이름을 갖는 변수로 만든 것

```cpp
TypeName arrName[n];
```

### 1차원 배열

<img src="/assets/img/blog/2024-10-13-cpp-array-pointer_01.png">

- float fArray[3]은 3개의 float 값을 저장하는 배열이며
- fArray[0], fArray[1], fArray[2] 3개의 저장공간은 메모리 내에 연속적으로 있다.
- fArray는 **배열 전체의 시작 주소**를 나타낸다.

### 2차원 배열

- 1차원 배열이 원소인 배열

<img src="/assets/img/blog/2024-10-13-cpp-array-pointer_02.png">

### 배열의 초기화

```cpp
int a[5] = { 1, 2, 3, 4, 5 }; // =는 생략 가능
int b[5] = { 1, 2, 3 }; // b[3]과 b[4]는 0으로 초기화됨
int c[] = { 1, 2, 3, 4, 5 }; // 배열의 크기는 5임
int d[2][4] = { { 1, 2, 3, 4 }, { 5, 6, 7, 8 } } // 2차원 배열
```

## 포인터

변수, 동적으로 할당된 메모리, 함수 등을 가리키는(주소를 저장하는) 변수

```cpp
TypeName* prtVar;
```

### 포인터 사용

```cpp
int a = 10;
int *ptr;

ptr = &a; // ptr에 a의 주소를 넣음
cout << "ptr의 값 : " << ptr << endl; // 000000093CF2FF(주소)
cout << "ptr가 가리키는 값 : " << *ptr << endl; // 10
*ptr = 20;
cout << "변수 a의 값 : " << a << endl; // 20
```

- `&a`는 변수 a의 주소를 나타낸다.
- 간접 액세스 연산자 \*를 포인터 변수 앞에 붙여 메모리의 값에 액세스 한다.
- ptr가 변수 a의 주소를 가리키고 있으므로 \*ptr를 사용하는 것은 변수 a를 사용하는 것과 마찬가지이다.

### 구조체 및 객체의 포인터

```cpp
struct C2dType { double x, y; };

C2dType point;
C2dType *c2dPtr = &point;
```

- 구조체 및 객체의 포인터의 항목에 액세스 하려면 `(*c2dPtr).x`처럼 포인터를 괄호로 감싸서 표기한다.
  - 멤버 선택 연산자 '.'의 우선순위가 간접 액세스 연산자 '\*'보다 높기 때문이다.
- 혹은 '->' 연산자를 사용하여 액세스 할 수 있다. ex) `c2dPtr->x`

### const 포인터

- const 한정어를 넣는 위치에 따라 의미가 달라진다.

```cpp
int a = 10, b = 20;
const int *ipt = &a;
*ipt = 30; // 에러
ipt = &b; // OK
```

```cpp
int a = 10, b = 20;
int* const ipt = &a;
*ipt = 30; // OK
ipt = &b; // 에러
```

```cpp
int a = 10
const int b = 20;
int *pt1 = &a; // OK
int *pt2 = &b; // 에러 - pt2로 b를 변경할 수 있음
const int *pt3 = &b; // OK - pt3를 변경할 수 없으므로 b도 변경할 수 없음
```

### char\* 포인터

```cpp
char str[14] = "Hello World!";
char *pt = str;
cout << pt << endl; // Hello World!
cout << *pt << endl; // H
```

- char\* 타입의 포인터는 해당 포인터가 가리키는 메모리 위치에서 시작하는 문자열을 가리킨다.
- C 스타일 문자열을 출력하면 마지막에 '\0'(널 종료 문자)를 만날 때까지 출력한다.
- char\* 타입에만 예외적인 동작이며 다른 타입에는 포인터 변수에 주소가 저장된다.

## 동적 메모리

- 프로그램 동작 중 필요한 공간만큼 기억공간을 할당하고 반환할 수 있다.
- 포인터 변수가 기억공간을 가리키게 하면 그 포인터를 이용해 액세스 할 수 있다.

#### 메모리 할당 연산자 new

```cpp
ptrVar = new TypeName;
ptrVar = new Typename[n]; // 배열
```

<img src="/assets/img/blog/2024-10-13-cpp-array-pointer_03.png">

#### 메모리 반환 연산자 delete

```cpp
delete TypeName;
delete [] Typename; // 배열
```

<img src="/assets/img/blog/2024-10-13-cpp-array-pointer_04.png">

## 참조

- 어떠한 대상을 가리키는 값 (포인터와 유사함)
- 참조 변수는 참조 대상의 별명처럼 사용할 수 있음
- l-value 참조 : 실체가 있는 대상에 대한 참조
- r-value 참조
  - 값을 사용한 후 그 값을 더 이상 가지고 있을 필요가 없는 대상을 참조
  - 객체의 값을 다른 객체로 이동하는 용도에 사용

```cpp
TypeName& refVar = varName;
```

- TypeName: 참조 대상의 자료형
- refVar: 참조 변수의 이름
- varName: 참조 대상

### 포인터와 다른 점

- 참조를 이용하여 값을 읽거나 저장할 때는 변수를 사용하는 형식과 동일하다.
  - 포인터처럼 '\*'과 같은 연산자를 사용하지 않는다.
- 참조 변수는 초기화를 통해 반드시 어떤 대상을 참조해야 하므로 무엇을 참조하고 있는 지 알 수 없는 상황은 발생하지 않는다.
  - 포인터는 초기화를 하지 않거나 가리키던 대상을 delete 함에 따라 무엇을 참조하고 있는 지 알 수 없는 상황이 발생할 수 있다.
- 참조 변수는 초기화를 통해 지정된 참조 대상을 바꿀 수 없어 참조의 유효기간 동안 하나의 대상만 참조할 수 있다.
  - 포인터는 const 한정어를 지정하지 않는 이상 다른 대상을 가리키도록 변경할 수 있다.

### const 참조

```cpp
int x { 10 };
const int& xRef = x;
xRef += 10; // 에러 - const 참조로 값을 수정할 수 없음
```
