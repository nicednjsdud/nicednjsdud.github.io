---
title: (Kotlin-Coroutine) 코루틴 이해하기 (2)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Kotlin
description: Kotlin
tag: Kotlin
article_tag1: Kotlin
article_section: Kotlin
meta_keywords: Kotlin, Back_end
last_modified_at: "2024-09-10 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

## Kotlin 코루틴 (Coroutine) 이해하기 - 2

## 목차

1. CoroutineScope (코루틴 스코프)
2. Dispatchers (디스패처)
3. 구조적 동시성 (Structured Concurrency)
4. Job과 Deferred

## 1. CoroutineScope (코루틴 스코프)

- 코루틴이 생성되고 관리되는 범위를 CoruntineScope라고 한다.
- 메모리 누수 및 관리 문제를 해결해주는 중요한 구조로, 코루틴의 생명주기를 관리한다.
- **launch** 또는 **async** 함수는 항상 CorountineScope안에서 실행되며, 이 스코프가 취소되면 해당 코루틴들도 모두 종료된다.

```java
fun main() = runBlocking {
    val job = launch {
        delay(1000L) // 비동기 작업
        println("코루틴 완료")
    }
    println("메인 스레드 실행 중...")
    job.join() // 코루틴이 끝날때 까지 대기
    println("메인 스레드 종료")
}
```

- 위 코드는 runBlocking을 사용해 코루틴을 실행하고, 스코프 내에서 laucnh를 통해 비동기 작업을 시작

## 2. Dispatchers (디스패처)

- 코루틴은 다양한 스레드에서 실행 될 수 있으며, 이를 제어하는 것이 **Dispachers**이다.
- 디스패처는 코루틴이 어느 스레드에서 실행될지를 결정하며, 다음과 같은 주요 옵션들이 있다.

### 1) Dispachers.Default

- CPU 집약적인 작업을 처리할 때 사용

### 2) Dispachers.IO

- 네트워크 요청이나 파일 입출력 같은 IO작업에 사용

### 3) Dispachers.Main

- UI 관련 작업에 사용 (주로 Android 개발)

```java
launch(Dispatchers.IO) {
    println("IO 작업 수행 중")
}

```

## 3. 구조적 동시성 (Structured Concurrency)

- 코루틴의 생명주기를 쉽게 관리할 수 있도록 설계된 개념
- 상위 코루틴이 종료되면 모든 하위 코루틴이 함께 종료되도록 하여, 누락된 작업이나 메모리 누수를 방지
- **CoroutineScope**는 이 구조적 동시성의 핵심

```java
fun main() = runBlocking {
    val job = async {
        delay(1000L)
        "결과"
    }
    println("데이터 처리 중...")
    println("결과: ${job.await()}")
}

```

## 4. Job과 Deferred

- Job은 코루틴의 상태를 나타내는 객체
- 코루틴이 실행, 완료, 취소 되었는지를 추적할 수 있고, 이를 통해 제어가능
- Deferred는 Job의 하위 타입으로, 비동기 작업이 결과를 반환할때 사용

```java
val job = launch {
    delay(1000L)
}
job.cancel()  // 코루틴 취소

```

- 위의 예시에서 **job.cancel()**을 통해 실행 중인 코루틴을 취소할 수 있습니다.
