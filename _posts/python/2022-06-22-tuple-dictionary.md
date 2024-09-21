---
title: "[Python 기초] Tuple, Dictionary 자료형"
categories: [Python]
tags: [python]
---

{:toc .large-only}

## Tuple 자료형

- 여러 자료를 함께 담을 수 있는 시퀀스 자료형

- 시퀀스 자료형이기 때문에 인덱스, 슬라이딩, in, len(), `+, *` 연산이 가능하다.

- **자료 추가, 삭제, 변경이 불가하다.**

- `()` 소괄호로 묶어서, 혹은 소괄호 없이 나열해서 표현

```python
tuple_zero = () # 빈 튜플
tuple_one = (1,) # 원소가 하나일 때는 꼭 , 기호를 넣어줘야 한다.
tuple_ = (1, 2, 3, 4, 5)
tuple_ = 1, 2, 3, 4, 5
```

## Dictionary 자료형

- `{key: value}` 형식의 자료형

- **key는 변할 수 없는 자료형이어야 한다.** 리스트는 key가 될 수 없다.

```python
person = {'name': 'Michael', 'age', 10}
print(person['name']) # Michael
print(person['age']) # 10
```

위 예제에서 key-value를 담은 변수 person를 Dictionary라 부른다.

#### 자료 추가

```python
person = {'name': 'Michael', 'age', 10}
person['hometown'] = 'Seoul'
# person = {'name': 'Michael', 'age', 10, 'hometown': 'Seoul'}
```

#### 자료 삭제

`del` 키워드로 Dictionary의 원소를 삭제할 수 있다.

```python
person = {'name': 'Michael', 'age', 10}
del person['age']
# person = {'name': 'Michael'}
```

#### keys/values 메서드

- `Dictionary.keys()` : Dictionary의 모든 Key를 반환
- `Dictionary.values()` : Dictionary의 모든 Value를 반환

#### 연습문제

| Coffee         | Price |
| -------------- | ----- |
| 아메리카노     | 4100  |
| 카페라떼       | 4600  |
| 카라멜마끼아또 | 5100  |

- 위 메뉴판대로 주문을 입력하면 총 금액을 출력하는 프로그램을 작성해봅시다.
- 첫번째 줄에 숫자 하나(n)를 입력받습니다.
- 두번째 줄부터 n+1번째 줄까지 메뉴(아메리카노, 카페라떼, 카라멜마끼아또)중 하나를 입력받습니다.

```python
n = int(input())
a = []
menu = {
    "아메리카노":4100,
    "카페라떼":4600,
    "카라멜마끼아또":5100
}
total = 0

while len(a) < n:
    s = input()
    if s in menu.keys():
        a.append(s)
    else:
        print("메뉴에 있는 음료만 시키십시오.")

for m in a:
    total += menu[m]

print(total)
```
