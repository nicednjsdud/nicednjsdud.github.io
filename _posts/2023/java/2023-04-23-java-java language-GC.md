---
published: true
title: (10분 테크톡) Java 57. GC (Garbege Collection)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-04-23 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# GC

## 목차

1. GC가 왜 필요하지?
2. GC 알고리즘
3. JVM의 GC
4. JVM GC 튜닝 맛보기

## 1. GC가 왜 필요하지?

- 프로그램이 **동적으로 할당했던 메모리 영역** 중 **필요 없게된 영역**을 알아서 해제

### 1) 장점

- 메모리 누수 방지
- 해제된 메모리 접근 방지
- 해제한 메모리 또 해제 방지

### 2) 단점

- GC작업은 순수 오버헤드
- 개발자는 언제 GC가 메모리를 해제하는지 모름

## 2. GC 알고리즘

- Root Space : 스택변수, 전역 변수등 heap 영억 참조를 담은 변수

### 1) Reference Counting

![alt](/assets/images/post/ComputerStudy/966.png)

- Heap 영역에 선언된 객체들이 각각 reference count라는 별도 숫자를 가지고 있다
- 여기서 reference count는 몇 가지 방법으로 해당 객체에 접근할 수 있는지를 뜻함
- 해당 객체에 접근할 수 있는 방법이 하나도 없다면, 즉, reference count가 0에 다다르면 가비지 컬렉션의 대상이 됨

#### 1-1) 한계점

- 순환 참조 문제

![alt](/assets/images/post/ComputerStudy/967.png)

- Root space애서의 Heap space 접근을 모두 끊는다고 가정
- 노란색 고리안의 객체들은 서로가 서로를 참조하기 있기 때문에 Reference count가 1로 유지
- 결국 사용하지 않은 메모리 영역이 해제되지 못하고 Memory Leak이 발생

### 2) Mark And Sweep

![alt](/assets/images/post/ComputerStudy/968.png)

- Referencce Counting의 순환 참조 문제를 해결 할 수 있다.
- 루트에서 부터 해당 겍체에 접근 가능한지를 해제의 기준으로 삼는다.
- 루트부터 그래프 순회를 통해 연결된 객체들을 찾아냄

![alt](/assets/images/post/ComputerStudy/969.png)

- 연결이 끊어진 객체들은 지우는 방식
- 연결이 되었다면 Reachable, 끊어졌다면 Unreachable이라고 불림
- Sweep이후에 분산되어 있던 메모리가 예쁘게 정리됨

![alt](/assets/images/post/ComputerStudy/970.png)

- 이를 메모리 파련화를 막은 Compaction이라고 함
- Compaction은 필수는 아님

#### 2-1) 단점

- 의도적으로 GC를 실행시켜야 한다.
- 어플리케이션 실행과 GC실행이 병행된다.

## 3. JVM의 GC - JVM 구조

- Java 8 기준

![alt](/assets/images/post/ComputerStudy/971.png)

### 1) JVM 메모리 구조

![alt](/assets/images/post/ComputerStudy/972.png)

- OS로부터 메모리를 할당 받은 후 해당 메모리를 용도에 따라 여러 영역으로 나누어서 관리
- 총 5가지 영역으로 나뉨

#### 1-1) Method Area

- 프로그램의 클래스 구조를 메타데이터처럼 가지며, 메서드의 코드들을 저장

#### 1-2) Heap

- 어플리케이션 실행 중에 생성되는 객체의 인스턴스를 저장하는 영역
- Garbage Collector에 의해 관리되는 영역

#### 1-3) Stack

- 메서드 호출을 스택 프레임이라는 블록으로 쌓으며 로컬 변수, 중간 연산 결과들이 저장되는 영역

#### 1-4) PC Register

- 쓰레드가 현재 실행할 스템프레임의 주소를 저장

#### 1-5) Native Method Stack

- C/C++ 등의 Low level 코드를 실행하는 스택

### 2) Root Space

![alt](/assets/images/post/ComputerStudy/973.png)

- Stack의 로컬 변수
- Method Area의 Static 변수
- Native Method Stack의 JNI 참조

### 3) JVM의 Heap 영역

![alt](/assets/images/post/ComputerStudy/974.png)

- JVM의 힙은 Young Generation과 Old Generation으로 나뉜다.
- Young Generation에서 발생하는 GC는 minor gc,
- Old Generation에서 발생하는 GC는 major gc라고 불린다.

#### 3-1) Young Generation

- Eden / survival 0 / survival 1 영역으로 나뉜다.
- Eden : 새롭게 생성된 객체들이 할당되는 영역
- Survival 영역은 minor gc로부터 살아남은 객체들이 존재하는 영역
- **Survival 0 또는 Survival 1은 둘중 하나는 반드시 비어있어야 함**

### 4) Stop The World

- GC를 싱행하기 위해 JVM이 어플리케이션 실행을 멈추는 것

### 5) JVM의 GC방식 살펴보기

#### 5-1) Serial GC

- 하나의 쓰레드로 GC를 실행
- Stop The World 시간이 긺
- 싱글 쓰레드 환경 및 Heap이 매우 작을 때 사용

![alt](/assets/images/post/ComputerStudy/975.png)

#### 5-2) Parallel GC

- 여러 개의 쓰레드로 GC를 실행
- 멀티코어 환경에서 사용
- Java 8의 default GC 방식

![alt](/assets/images/post/ComputerStudy/976.png)

#### 5-3) CMS GC (Concurrent-Mark-Sweep)

- Stop The World 최소화를 위해 고안
- GC 작업을 어플리케이션과 동시에 실행

![alt](/assets/images/post/ComputerStudy/977.png)

- Compation이 기본 제공이 되지않음
- G1 GC 등장에 따라 CMS GC는 대체 되었음

#### 5-4) G1 GC

![alt](/assets/images/post/ComputerStudy/978.png)

- Garbage First (G1)
- Heap을 Region으로 나누어 사용
- Java 9 부터 default GC 방식

## 4. JVM GC 튜닝 맛보기

- 성능 개선의 최종 단계

### 1) 목표

- Lod Generation으로 넘어가는 객체 최소화 하기
- Major GC 시간을 짧게 유지하기

### 2) 튜닝과정

- GC 상태 모니터링 하기
- 알맞은 GC 방식과 메모리 크기 설정
- 적용하기

### 3) Heap 크기 설정

- Xms : JVM 시작시 힙 영역의 크기
- Xmx : 최대 힙 영역 크기

### 4) Neq 영역의 크기 설정

- -XX:NewRatio: New 영역과 Old 영역의 비율
  - -XX:NewRatio 1 : **(New 영역 : Old 영역 == 1:1)**
  - -XX:NewRatio 2 : **(New 영역 : Old 영역 == 1:2)**
- -XX:NewSize : New 영역의 크기
- -XX:SurvivorRation : Eden 영역과 Survivor 영역의 비율

### 5) GC 실행 방식 설정

- -XX : +UseSerialGC : **SerialGC 사용**
- -XX : ParallelGCThreads = value : **ParallelGC 사용**
- -XX : +UseParallelOldGC : **ParallelGC + Compation**
- -XX : +UseGMSInitialingOccupancyOnly : **CMS GC 사용**
- -XX : +UseG1GC : **G1 사용**

## 출처

<a href="https://www.youtube.com/watch?v=FMUpVA0Vvjw">조웰의 GC</a>
