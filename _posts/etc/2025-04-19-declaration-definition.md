---
title: "선언(declaration)과 정의(definition)"
categories: [기타]
tags: [선언, 정의]
---

{:toc .large-only}

항상 헷갈려서 클로드에게 물어봄

### 선언(Declaration)

프로그램에게 "이런 이름의 것이 존재할 것이다"라고 알려주는 것입니다.

이름, 타입, 특성 등을 명시하지만 실제 메모리 할당이나 구현은 포함하지 않습니다

예: `int number;` (변수 선언), `void doSomething();` (함수 선언)

### 정의(Definition)

선언된 것에 대한 실제 구현이나 메모리 할당을 포함합니다.

예: `int number = 5;` (변수 정의 - 메모리 할당 포함)

함수의 경우: `void doSomething() { /* 코드 내용 */ }` (함수 정의 - 실제 구현 포함)

Java에서는 이 두 개념이 종종 동시에 이루어지기도 합니다. 예를 들어 `int x = 10;`은 변수 x를 선언하고 동시에 정의하는 것입니다.
