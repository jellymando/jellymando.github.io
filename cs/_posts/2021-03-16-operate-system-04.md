---
layout: post
title: 'CPU 스케줄링'
sitemap: false
---

{:toc .large-only}

## CPU 스케줄링

### 스케줄링의 개요

CPU 스케줄러는 프로세스가 생성된 후 종료될 때까지 모든 상태 변화를 조정하는 일을 한다.

### 스케줄링의 단계

- 고수준 스케줄링 : 시스템 내의 전체 프로세스 수를 조절
- 중간 수준 스케줄링 : 전체 시스템의 활성화된 프로세스 수를 조절하여 과부하를 막음
- 저수준 스케줄링 : 어떤 프로세스에 CPU를 할당할지, 어떤 프로세스를 대기 상태로 보낼지 등을 결정

### 스케줄링의 목적

- 공평성 : 모든 프로세스가 자원을 공평하게 배정받아야 하며, 자원 배경 과정엣어 특정 프로세스가 배제되어서는 안 된다.
- 효율성 : 시스템 자원이 유휴 시간 없이 사용되도록 스케줄링을 하고, 유휴 자원을 사용하려는 프로세스에는 우선권을 주어야 한다.
- 안정성 : 우선순위를 사용하여 중요 프로세스가 먼저 작동하도록 배정함으로써 시스템 자원을 점유하거나 파괴하려는 프로세스로부터 자원을 보호해야 한다.
- 확장성 : 프로세스가 증가해도 시스템이 안정적으로 작동하도록 조치해야 한다. 또한 시스템 자원이 늘어나는 경우 이 혜택이 시스템에 반영되게 해야 한다.
- 반응 시간 보장 : 응답이 없는 경우 사용자는 시스템이 멈춘 것으로 가정하기 때문에 시스템은 적절한 시간 안에 프로세스의 요구에 반응해야 한다.
- 무한 연기 방지 : 특정 프로세스의 작업이 무한히 연기되어서는 안 된다.

## 스케줄링 시 고려 사항

### 선점형 스케줄링과 비선점형 스케줄링

- 선점형 스케줄링 : 어떤 프로세스가 CPU를 할당받아 실행 중이더라도 운영체제가 CPU를 강제로 빼앗을 수 있는 스케줄링 방식
- 비선점형 스케줄링 : 어떤 프로세스가 CPU를 점유하면 다른 프로세스가 이를 빼앗을 수 없는 스케줄링 방식

### 프로세스 우선순위

우선순위가 높은 프로세스 : 커널 프로세스, 전면 프로세스, 대화형 프로세스, 입출력 집중 프로세스
우선순위가 낮은 프로세스 : 일반 프로세스, 후면 프로세스, 일괄 작업 프로세스, CPU 집중 프로세스

## 다중 큐

### 준비 상태의 다중 큐

준비 상태에서는 우선순위에 따라 다중 큐를 운영한다. 한 번에 하나의 프로세스를 꺼내어 CPU를 할당한다.

### 대기 상태의 다중 큐

대기 상태에서는 같은 입출력을 요구한 프로세스를 모아 다중 큐를 운영한다. 여러 개의 프로세스 제어 블록을 동시에 꺼내어 준비 상태로 옮긴다.

## 스케줄링 알고리즘

- FCFS 스케줄링 : 준비 큐에 도착한 순서대로 CPU를 할당하는 비선점형 스케줄링 방식
  - 콘보이 효과 : 처리 시간이 긴 프로세스가 CPU를 차지하면 다른 프로세스들은 하염없이 기다려 시스템의 효율성이 떨어짐
- SJF 스케줄링 : 준비 큐에 있는 프로세스 중에서 실행 시간이 가장 짧은 작업부터 CPU를 할당하는 비선점형 방식
  - starvation(아사 현상) : 작업 시간이 길다는 이유만으로 계속 뒤로 밀린다면 공평성이 현저히 떨어진다.
- HRN 스케줄링 : CPU를 할당받기 위해 기다린 시간과 CPU 사용 기간을 고려하여 스케줄링을 하는 비선점형 방식
- 라운드 로빈 스케줄링 : 한 프로세스가 할당받은 시간(타임 슬라이스) 동안 작업을 하다가 작업을 완료하지 못하면 준비 큐의 맨 뒤로 가서 자기 차례를 기다리는 선점형 방식
  - 시간 할당을 잘 조절하지 않으면 콘보이 효과나 starvation이 일어날 수 있다.
- STR 스케줄링 : 기본적으로 라운드 로빈 스케줄링을 사용하지만, CPU를 할당받을 프로세스를 선택할 때 남아 있는 작업 시간이 가장 적은 프로세스를 선택하는 선점형 방식
- 우선순위 스케줄링 : 프로세스는 중요도에 따라 우선순위를 갖는데 이러한 우선순위를 반영하여 CPU를 할당하는 방식
- 다단계 큐 스케줄링 : 우선순위에 따라 준비 큐를 여러 개 사용하는 비선점형 방식
- 다단계 피드백 큐 스케줄링 : 다단계 큐 스케줄링과 기본적인 형태가 같지만, CPU를 사용하고 난 프로세스가 원래의 큐로 되돌아가지 않고 우선순위가 하나 낮은 큐의 끝으로 들어간다.