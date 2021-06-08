---
layout: post
title: "자료구조 : 스택(Stack), 큐(Queue), 덱(Deque)"
sitemap: false
---

{:toc .large-only}

## 스택 (Stack)

<img src="/assets/img/blog/stack-queue-deque_01.png">

- LIFO (Last In First Out) : 후입선출 구조
- 한쪽 끝에서만 자료를 넣고 뺄 수 있는 접시처럼 쌓아올린 형태의 구조
- 삽입 (Push) : top에 데이터가 저장된다.
- 삭제 (Pop) : top의 데이터가 삭제된다.
- 자료가 없을 때 pop 하는 오류를 `stack underflow`, 스택의 크기 이상의 자료를 push 하려고 할 때의 오류를 `stack overflow`라고 한다.

#### 시간복잡도

- Insertion O(1)
- Deletion O(1)
- Search O(n)

삭제나 삽입시 맨 위에 데이터를 삽입하거나 삭제하기 때문에 시간복잡도는 늘 `O(1)`의 시간복잡도를 가진다.

하지만 특정 데이터를 찾을 때는 특정 데이터를 찾을 때까지 수행을 해야하므로 `O(n)`의 시간 복잡도를 가집니다.

#### Stack 활용 예시

- 재귀 알고리즘에서 유용하게 사용
- 역추적을 해야할 때 (ex. 문서 작업 시 실행 취소, 방문기록 뒤로 가기)
- 괄호 검사, 역순 문자열 만들기, 후위 표기법으로의 변환

## 큐 (Queue)

<img src="/assets/img/blog/stack-queue-deque_02.png">

- FIFO (First In First Out) : 선입선출 구조
- 한쪽 끝에서 삽입 작업이, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어지는 줄서서 기다리는 구조
- Enqueue : 큐 맨 뒤에 데이터 추가
- Dequeue : 큐 맨 앞쪽의 데이터 삭제
- head : dequeue 하였을 시 출력이 되는 부분 (유의어: front, first 등)
- tail : enqueue 하였을 시 입력이 되는 부분 (유의어: rear, back, last 등) // 다양하게 불린다.

#### 시간복잡도

- Insertion O(1)
- Deletion O(1)
- Search O(n)

#### Stack 활용 예시

- 우선순위가 같은 작업 예약
- 데이터를 입력된 순서대로 처리해야 할 때
- 너비 우선 탐색(BFS, Breadth-First Search) 구현
- 은행 업무, 콜센터 대기

## 덱 (Deque)

<img src="/assets/img/blog/stack-queue-deque_03.png">

- Deque (Double Ended Queue)
- 스택과 큐의 연산을 합쳐놓은 것이다.
- queue와 비슷하지만 deque는 front와 end에서 삭제와 삽입이 모두 가능하다.
- 여러 개의 메모리 단위로 데이터를 저장
- 크기가 가변적이다. (선언 후에 변경할 수 있다.)

#### Deque 활용 예시

- 앞과 뒤에서 삽입, 삭제가 자주 일어나는 경우
- 데이터의 개수가 가변적일 경우
- 데이터 검색을 거의 하지 않을 경우 (랜덤 요소에 접근해야 할 때)

[[자료구조] 스택(Stack), 큐(Queue), 덱(Deque)](https://velog.io/@choiiis/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack%EA%B3%BC-%ED%81%90Queue)<br/>
[[자료구조] 스택 (STACK), 큐(QUEUE) 개념/비교 /활용 예시](https://devuna.tistory.com/22)<br/>
[스택, 큐 (Stack, Queue)](https://velog.io/@sbinha/%EC%8A%A4%ED%83%9D-%ED%81%90)
