---
published: true
title: (10분 테크톡) Java 54. Blocking vs Non-Blocking, Sync vs Async
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Java 54. Blocking vs Non-Blocking, Sync vs Async
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-03-12 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Blocking vs Non-Blocking, Sync vs Async

## 목차

1. Blocking vs Non - Blocking
2. Synchronous vs Asynchronous
3. 조합 4가지 경우
4. 정리

## 1. Blocking vs Non - Blocking

### 1) Blocking

- 자신의 작업을 진행하다가 다른 주체의 작업이 시작되면 다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 것

### 2) Non - Blocking

- 다른 주체의 작업에 관련없이 자신의 작업을 하는 것

### 3)

- 다른 주체가 작업할 때 자슨의 **제어권**이 있는지 없는지로 볼 수 있다.

## 2. Synchronous vs Asynchronous

### 1) Synchronous

- 번역을 해보면 동기라는 뜻을 가진다.
- 작업을 동시해 수행하거나, 동시에 끝나거나, **끝나는 동시에 시작함을 의미**

### 2) Asynchronous

- 번역을 해보면 비동기라는 뜻을 가진다.
- 시작, 종료가 일치하지 않으며, **끝나는 동시에 시작을 하지 않음**을 의미

### 3)

- 결과를 돌려주었을 때 **순서와 결과에 관심**이 있는지 아닌지로 판단할 수 있다.

## 3. 4가지 조합의 경우

![alt](/assets/images/post/ComputerStudy/876.png)

### 1) Blocking/Sync

- Blocking의 관점은 제어권에 있다.

  - 다른 작업이 시작되는 동안 동작하지 않음

- Sync의 관점은 결과의 처리이다.
  - 따라서 결과를 반환하면 해당 업무를 바로 처리하게 됨

```java
  import java.util.Scanner;

  public class Application {

    public static void main(String[] args){

      System.out.print("출력하고 싶은 메세지를 입력하세요 : ");
      final Scanner scanner = new Scanner(System.in);
      String message = scanner.nextLine();
      System.out.println("블로킹 동기");
      System.out.println(message);
    }
  }
```

![alt](/assets/images/post/ComputerStudy/877.png)

- 제어권이 넘어갔기 때문에 위 내용이 실행이 되지않고 있다.

![alt](/assets/images/post/ComputerStudy/878.png)

- 입력하면 제어권과 결과를 같이 받아서 처리한다.

### 2) Non-Blocking/Sync

- Non-Blocking : 다른 작업이 있어도 자신의 제어권을 가지고 일을 하는 것
- Sync : 결과에 관심이 있는 것
- Blocking/Sync와 큰 차이가 없다.

```c
  private float _progreess = 0.0f;

  void IEnumberator GetResourceData(){
    WWW www = new WWW("url");
    while(!www.isDone){
        _progreess = www.progreess;
        //화면에 progreses를 표시할 코드 호출
    }
    {
      // 화면 전환 코드
    }
  }
```

- 게임에서 맵을 넘어갈때 얼마만큼 로딩이 있는지 보여줄때 사용

### 3) Blocking/Async

- Blocking 이기 때문에 자신의 작업에 대한 제어권이 없다.

### 4) Non-Blocking/Async

- Non-Blocking은 다른 작업이 시작되어도 자신이 하던 작업을 멈추지 않는다.
  - 따라서 양쪽에서 서로 각자 작업을 처리하게 됨
- Async는 결과를 바로 처리하는게 아니다.
  - 따라서 다른 작업에서 끝난 결과를 바로 처리하지 않고, 자기 일이 끝나게 되면 그때야 처리를 하게 됨

```java
  fetch('url', option)
    .then((response) => {
      return response.json();
    })
    .then((data) => {
      something(data);
    });
```

- 대표적인 예시로 자바스크립트에서 API요청을 하고 다른 작업을 하다가 콜백을 통해서 추가적인 작업을 처리를 할 때

## 4. 정리

### 1) Blocking VS Non - Blocking

- 둘을 보면 비슷한데 바라보는 관점에서 차이가 있다.
  - 제어의 관점에서 바라보는 것

### 2) Sync VS Async

- 결과의 관점과 순서의 관점에서 바라보는 것이다.

## 출처

<a href="https://www.youtube.com/watch?v=oEIoqGd-Sns">멍토의 Blocking vs Non - Blocking, Sync vs Async</a>
