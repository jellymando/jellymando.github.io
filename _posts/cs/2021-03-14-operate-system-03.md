---
title: '프로세스와 스레드'
categories: [Computer Science]
tags: [cs, os]
---

{:toc .large-only}

## 프로세스와 스레드

### 프로세스의 개요

1. 프로세스의 개념

프로그램은 저장장치에 저장되어 있는 정적인 상태이고, 프로세스는 실행을 위해 메모리에 올라온 동적인 상태이다.
프로세스는 컴퓨터 시스템의 작업 단위로 태스크(task)라고도 부른다.

2. 프로그램에서 프로세스로의 전환

프로그램이 프로세스가 되려면 메모리에 올라오는 것과 동시에 프로세스 제어 블록이 생성되어야 한다.
프로세스 제어 블록에 있는 다양한 정보 중 대표적인 세 가지는 다음과 같다.

- 프로세스 구분자 : 각 프로세스를 구분하는 구분자
- 메모리 관련 정보 : 프로세스의 메모리 위치 정보. 메모리 보호를 위한 경게 레지스터와 한계 레지스터도 포함되어 있다.
- 각종 중간값 : 프로세스가 사용했던 중간값. 다음에 작업해야 할 코드의 위치가 담긴 레지스터인 프로그램 카운터가 저장된다.

3. 프로세스의 상태

- 생성 상태 : 프로그램을 메모리에 가져와 실행 준비가 완료된 상태
- 준비 상태 : 프로세스가 자기 차례를 기대리는 상태. CPU 스케줄러가 dispatch를 실행하면 실행 상태로 바뀐다.
- 실행 상태 : 선택된 프로세스가 타임 슬라이스 언어를 얻어 CPU를 사용하는 상태. 프로세스 사이의 문맥 교환이 일어난다.
- 대기 상태 : 실행 상태에 있는 프로세스가 입출력을 요청하면 입출력이 완료될 때까지 기다리는 상태. 입출력이 완료되면 준비 상태로 간다.
- 완료 상태 : 프로세스가 종료된 상태. 사용하던 모든 데이터가 정리된다. 정상 종료인 exit와 비정상 종료인 abort를 포함한다.

- 휴식 상태 : 프로세스가 작업을 일시적으로 쉬고 있는 상태. 유닉스에서 Ctrl+Z
- 보류 상태 : 프로세스가 메모리에서 잠시 쫓겨난 상태. (일시 정지 상태)
    - 메모리가 꽉 차서 일부 프로세스를 메모리 밖으로 내보낼 때
    - 프로그램에 오류가 있어서 실행을 미루어야 할 때
    - 바이러스와 같이 악의적인 공격을 하는 프로세스라고 판단될 때
    - 매우 긴 주기로 반복되는 프로세스라 메모리 밖으로 쫓아내도 큰 문제가 없을 때
    - 입출력을 기다리는 프로세스의 입출력이 계속 지연될 때

### 프로세스 제어 블록과 문맥 교환

1. 프로세스 제어 블록

프로세스를 실행하는 데 필요한 중요한 정보를 보관하는 자료 구조로, 모든 프로세스는 고유의 프로세스 제어 블록을 가진다.
프로세스 생성 시 만들어져서 프로세스가 실행을 완료하면 폐기된다.

2. 문맥 교환

CPU를 차지하던 프로세스가 나가고 새로운 프로세스를 받아들이는 작업.
두 프로세스의 프로세스 제어 블록 및 이와 관련된 값들을 교환.
한 프로세스가 자신에게 주어진 시간을 다 사용하면 발생하고, 인터럽트가 걸렸을 때도 발생한다.

### 프로세스의 연산

1. 프로세스의 구조

- 코드 영역 : 프로그램의 본문이 작성된 곳으로 텍스트 영역이라고도 한다.
프로그래머가 작성한 프로그램은 코드 영역에 탑재되며 탑재된 코드는 읽기 전용으로 처리된다.
- 데이터 영역 : 코드가 실행되면서 사용하는 변수가 파일 등의 각종 데이터를 모아놓은 곳. 읽기와 쓰기 가능
- 스택 영역 : 운영체제가 프로세스를 실행하기 위해 부수적으로 필요한 데이터를 모아놓은 곳.
프로세스 내에서 함수를 호출하면 함수를 수행하고 원래 프로그램으로 되돌아올 위치를 이 영역에 저장한다.

2. 프로세스의 생성과 복사

- fork() 시스템 호출 : 실행 중인 프로세스로부터 새로운 프로세스를 복사하는 함수
    - 프로세스의 생성 속도가 빠르다.
    - 추가 작업 없이 자원을 상속할 수 있다.
    - 시스템 관리를 효율적으로 할 수 있다.

3. 프로세스의 전환

- exec() 시스템 호출 : 기존의 프로세스를 새로운 프로세스로 전환하는 함수. 이미 만들어진 프로세스의 구조를 재활용한다.
    - 기존의 프로세스 구조를 그대로 둔 채 내용만 바꾸어 새로 실행
    - 각종 프로세스 구분자만 남겨두고 프로세스의 나머지 내용을 새로운 것으로 바꾼다.

4. 프로세스의 계층 구조

부모 프로세스를 복사하여 자식 프로세스를 만드는 방법으로 프로세스끼리 계층 구조를 갖는 것을 말한다.
유닉스 운영체제는 init 프로세스를 만든 다음 나머지 프로세스를 init 프로세스의 자식으로 만들어 트리 구조를 이룬다.

- 프로세스 계층 구조의 장점
    - 여러 작업의 동시 처리
    - 용이한 자원 회수

- 고아 프로세스 : 부모 프로세스가 자식보다 먼저 죽는 경우에 발생
- 좀비 프로세스 : 자식 프로세스가 종료 했음에도 부모가 뒤처리를 하지 않을 때 발생

## 스레드

1. 스레드의 개념

프로세스의 코드에 정의된 절차에 따라 CPU에 작업 요청을 하는 실행 단위이다.

- 프로세스와 스레드의 차이
    - 프로세스는 요리 작업 전체와 같고, 스레드는 요리를 완성하기 위해 수행하는 각각의 조리에 해당
    - 프로세스끼리는 약하게 연결되어 있는 반면 스레드끼리는 강하게 연결되어 있다.

- 스레드 관련 용어
    - 멀티스레드 : 프로세스 내 작업을 여러 개의 스레드로 분할함으로써 작업의 부담을 줄이는 프로세스 운영 기법
    - 멀티태스킹 : 운영체제가 CPU에 작업을 줄 때 시간을 잘게 나누어 배분하는 기법
    - 멀티프로세싱 : CPU를 여러 개 사용하여 여러 개의 스레드를 동시에 처리하는 작업 환경
    - CPU 멀티스레드 : 파이프라인 기법을 이용하여 동시에 여러 스레드를 처리하도록 만든 병렬 처리 기법

2. 멀티스레드의 장단점

- 멀티스레드의 장점
    - 응답성 향상
    - 자원 공유
    - 효율성 향상
    - 다중 CPU 지원

- 멀티스레드의 단점
    - 멀티스레드의 경우 모든 스레드가 자원을 공유하기 때문에 한 스레드에 문제가 생기면 전체 프로세스에 영향을 미친다. ex) 익스플로러는 문제가 있는 화면을 강제로 종료하면 익스플로러 전체가 종료된다.

3. 멀티스레드 모델

- 사용자 스레드 : 사용자 레벨에서 관련 라이브러리를 사용하여 구현
- 커널 스레드 : 커널이 멀티스레드를 지원하는 방식
- 멀티레벨 스레드 : 사용자 스레드와 커널 스레드를 혼합한 방식으로 하이브리드 스레드라고도 한다.