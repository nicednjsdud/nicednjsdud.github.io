---
published: true
title: (10분 테크톡) Java 53. 멀티 스레드와 동기화 in Java
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Java 53. 멀티 스레드와 동기화 in Java
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-03-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 멀티 스레드와 동기화 in Java

## 목차

- 공유자원과 임계영역
- 경쟁상태
- 원자성과 가시성
- 동기화
  - 블로킹
  - 논블로킹
- 스레드 안전한 객체 설계 방법

## 1. 공유자원과 임계영역

- 공유자원 : 여러 스레드가 동시에 접근할 수 있는 자원
- 임계영역 : 공유자원들 중 여러 스레드가 동시에 접근했을때 문제가 생길 수 있는 부분

![alt](/assets/images/post/ComputerStudy/859.png)

### 1) 경쟁 상태

- 둘 이상의 스레드가 공유자원을 병행적으로 읽거나 동작할 때 타이밍이나 접근 순서에 따라 결과가 달라지는 상황
- ex) Read - Modify - Write, Check - then - act

#### 1-1) Read - Modify - Write

- 30명의 수강생이 동시에 신청하게 된다면?

```java
  @RestController
  @RequestMapping("/race-condition")
  public class RaceConditionController {

    public static Integer studentCount = 0;

    @PostMapping("/1/increase")
    public ResponseEntity<Void> increaseCount(){
      studentCount++;
      return ResponseEntity.ok().build();
    }

    @GetMapping("/1/count")
    public ResponseEntity<Integer> getCount(){
      return ResponseEntity.ok(studentCount);
    }
  }
```

![alt](/assets/images/post/ComputerStudy/860.png)

#### 1-2) Check - then - act

- 수강 신청후에 숫자를 세서 30명 미만이면 폐강 위험 경고문을 출력하는 메소드를 동시에 100명이 요청한다면?

```java
  @PostMapping("/2/check-then-act")
  public ResponseEntity<Void> printWarning() throws InterruptedException {
    studentCount++;
    if(studenctCount < 30){
      Thread.sleep(1);
      System.out.println("폐강위험! studentCount = " + studentCount);
    }
    return ResponseEntity.ok().build();
  }
```

![alt](/assets/images/post/ComputerStudy/861.png)

- if 분기를 통과하기 전에는 적합한 숫자였지만 if 분기문을 통과한 후에는 조건에 부합하지 않은 숫자가 된다.
- 그래서 이런 경쟁 상태가 발생
  - 방지하기 위해서 **원자성과 가시성**이라는 것을 보장해야 함

## 2. 원자성

### 1) 원자성이란?

- 공유 자원에 대한 작업의 단위가 더 이상 쪼갤 수 없는 하나의 연산인 것처럼 동작하는 것

#### 1-1) Read - Modify - write 예제

1. 메모리에서 값을 읽어옴 (read)
2. 읽어온 값을 수정 (modify)
3. 수정한 값을 다시 메모리에 덮어씀 (write)

#### 1-2) Check - then - act 예제

1. 분기문 비교 (read)
2. 로직 (act)

## 3. 가시성

- 메인 메모리에 있는 진짜 값을 보지 못해서 가시성 이라고 한다.
- 가시성을 알기위해서는 CPU 캐시 메모리에 대해서 알아야함
- 수정 예정 \*
- 자바에서는 volatile 이라는 메서드를 제공

## 4. 동기화

### 1) 블로킹

- 특정 스레드가 작업을 수행하는 동안 다른 작업은 진행하지 않고 대기하는 방식
- Ex) Monitor, Synchronized 키워드

#### 1-1) 모니터

- 자바에서 동기화를 하기 위한 도구
- 배타동기는 synchronized, 조건동기는 wait(), notify(), notifyAll()

![alt](/assets/images/post/ComputerStudy/862.png)

- 임계영역에는 한번에 한 쓰레드만 락을 가지고 들어가도록 설계가 되어 있다.
- 만약에 임계영역에 접근하는 여러 쓰레드가 있다면 그중에 한 쓰레드가 먼저 임계영역에 들어갈 수 있다.

![alt](/assets/images/post/ComputerStudy/863.png)

- 작업을 수행하다가 만약에 wait() 라는 연산을 만나면 이 쓰레드는 슬립 상태가 되면서 조건 동기 큐로 들어감

![alt](/assets/images/post/ComputerStudy/864.png)

- 배타 동기큐에 있던 다른 쓰레드들이 임계영역이 비었기 때문에 임계영역에 락을 가지고 들어감

![alt](/assets/images/post/ComputerStudy/865.png)

- 작업을 수행하다가 만약에 notify()나 notifyAll() 이라는 메서드를 호출을 하게 되면 조건 동기 큐에서 자고 있던  
  쓰레드가 깨어나게 되면서 임계 영역이 비었을 때 다시 임계영역으로 돌아와서 작업을 수행하게 함

![alt](/assets/images/post/ComputerStudy/866.png)

- 이런 메커니즘을 모니터 메커니즘이라고 함

#### 1-2) Synchronized

- 배타 동기를 선언하는 키워드
- 연산결과가 메모리에 써질때까지 다른 쓰레드는 대기

```java
  @PostMapping("/2/check-then-act")
  public synchronized ResponseEntity<Void> printWarning() throws InterruptedException {
    studentCount++;
    if(studenctCount < 30){
      Thread.sleep(1);
      System.out.println("폐강위험! studentCount = " + studentCount);
    }
    return ResponseEntity.ok().build();
  }
```

- 앞서 보았던 수강신청 경고 예제에 Synchronized를 붙여서 실행한다면?

![alt](/assets/images/post/ComputerStudy/867.png)

- 예상했던 결과를 얻음

##### 1-3) Synchronized 동작 방식

![alt](/assets/images/post/ComputerStudy/868.png)

- 임계구역에 한개의 쓰레드만 들어올 수 있기 때문에 이 쓰레드가 다 들어오고 나서 자기가 연산할 것을 다 연산 하고  
  메인 메모리에 반영시킨 이후에 임계구역에서 나가게 된다.

![alt](/assets/images/post/ComputerStudy/869.png)

- 그러고 다음 쓰레드가 임계구역에 들어오게 되고 들어올 때는 메인 메모리에서 이미 동기화된 값을 읽어오기 때문에  
  아까와 같은 문제발생하지 않음
- 이런 순차접근으로 **원자성 + 가시성**을 보장

##### 1-4) 블로킹 방식의 단점

- 하나의 쓰레드만 임계구역에서 작업을 수행할 수 있기 때문에 나머지 대기하는 쓰레드들이 발생을 함
  - 성능저하로 이어짐
- 임계구역에 들어갈 때 락을 획득하고 들어가기 때문에 데드락 이라는 문제가 발생 할 수 있다.

### 2) 논블로킹

- 다른 스레드의 작업여부와 상관없이 자신의 작업을 수행하는 방식
- Ex) Atomic 타입

#### 2-1) CAS (Compare and Set)

![alt](/assets/images/post/ComputerStudy/870.png)

- 자원값 : 연산 하고자 하는 값
- 기댓값 : 자원값과 똑같은 값을 만듬
- 새로운 값 : 이 기대값을 기반으로 연산을 진행을 해서 새로운 값을 도출

![alt](/assets/images/post/ComputerStudy/871.png)

- 내가 이전에 만들었던 기대값과 현재의 자원값이 같은 지를 한번 확인하는 로직
- 만약 자원값 = 기대값 이면 새로운 값으로 수정을 하고 true 반환
- 만약 내가 연산하는 동안 이 자원 값이 달라져서 자원값 != 기대값이면 수정을 하지 않고 false로 반환

#### 2-2) Atomic 타입

- 동시성을 보장하기 위해서 자바에서 제공하는 Wrapper Class
- CAS + Volatile

![alt](/assets/images/post/ComputerStudy/872.png)

- 보통 일반적인 쓰레드 에서는 값을 연산을 하고자 할 때 연산하는 값을 끌어올 때는 JVM과 CPU 사이에 있는  
  캐시 값에서 변수를 끌어옴

![alt](/assets/images/post/ComputerStudy/873.png)

- 근데 아토믹 레퍼런스를 설정하게 되면 JVM 메모리에서 바로 쓰레드로 값을 당겨 올 수 있다.
- 바로 값을 당겨와 가지고 연산을 진행을 하게 된다.
  - 연산을 할 때는 compareAndSet() 이라는 메서드가 호출이 된다.
  - 현재 메모리에 저장된 값과 쓰레드 내부의 내가 이미 만들어놨던 기대값을 비교해서
  - 만약 일치를 하면 true
  - 불일치 하면 false
- **아토믹 레퍼런스가 volatile을 통해서 가시성을 그리고 CAS를 통해서 원자성을 보장한다.**

#### 2-3) AtomicInteger

- 앞서 보았던 수강신청 예제에 AtomicInteger를 적용한다면?

```java
  @RestController
  @RequestMapping("/atomic")
  public class AtomicController {

    private AtomicInteger studentCount = new AtomciInteger(0);

    @PostMapping("/increase")
    public ResponseEntity<Void> increaseAtomicCount(){
      studentCount.addAndGet(1);
      return ResponseEntity.ok().build();
    }

    @GetMapping("/count")
    public ResponseEntity<AtomicInteger> getStudentCount(){
      return ResponseEntity.ok(studentCount);
    }
  }
```

- 기대했던 기댓값이 나옴

![alt](/assets/images/post/ComputerStudy/874.png)

- AtomicInteger가 먼저 원자성하고 가시성을 보장해서 동기화가 잘돼 가지고 정상적인 값이 나오게 됨

## 5. 스레드 안전한 객체란?

- 여러 스레드가 동시에 클래스를 사용하려고 하는 상황에서 클래스 내부의 값을 안정적인 상태로 유지할 수 있다.

### 1) 스레드 안전한 객체를 설계하는 법

![alt](/assets/images/post/ComputerStudy/875.png)

- 굉장히 많다..
- 가장 확실하고 안전하고 간단한 방법은 공유 변수를 최대한 안 두는게 최선
- 공유변수 최소화 + 캡슐화 + 문서화 잘하자.
- 불가피하게 써야한다면 내가 관리해야 될 포인트를 한 곳에 모아서 한 객체에서 캡슐화를 해가지고 그 객체만 관리할 수  
  있게끔 하는게 차선
- 공유변수를 사용하게 되면 동기화 정책을 많이 적용을 하게 될 탠데 그런 동기화 정책이 코드에 들어가면 코드 파악이 어려워짐
  - 이런것을 알려주기 위해서 문서화를 잘 해놓는 것도 중요

## 출처

<a href="https://www.youtube.com/watch?v=ktWcieiNzKs">알렉스, 열음의 멀티스레드와 동기화 In Java</a>
