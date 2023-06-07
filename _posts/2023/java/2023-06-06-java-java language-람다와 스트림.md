---
published: true
title: (10분 테코톡) Java 61. 람다
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
last_modified_at: "2023-06-06 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 람다와 스트림

## 목차

### 1) 람다

- 람다식이 뭐야?
- 람다식은 함수형 인터페이스를 구현한 인스턴스라고?
- 남이 잘 만들어놓은 표준 함수형 인터페이스를 쓰는걸 추천해
- 메서드 참조를 하면 좀더 코드가 깔끔해질껄?


## 1. 람다

### 1) 람다식이 뭐야?

* 메서드를 하나의 식으로 표현한 식

```java
  int addOperation(int a, int b){
    return a + b;
  }

  ---

  (int a, int b) -> a + b
```

* Runnable라고 하는 함수형 인터페이스

#### 1-1) 함수형 인터페이스 ?

* 함수형 인터페이스 = 추상 메서드가 딱 1개만 있는 인터페이스
* default 메서드와 static 메서드는 존재할 수 있다.

```java
  package bridge;

  @FunctionInterface
  public interface BridgeNumberGenerator {

    int generate(); // 추상 메서드
  }
```

* 추상메서드를 오버라이딩해서 클래스를 만든다. 
* 이클래스로부터 인스턴스를 생성할 수 있다.

```java
  public class BridgeRandomNumberGenerator implements BridgeNumberGenerator {

    @Override
    public int generate(){
      return new Random().nextInt();
    }
  }
```

* 람다식을 사용해 인스턴스를 만들 수 있다.

```java
  BridgeNumberGenerator bridgeRandomNumberGenerator = () -> new Random().nextInt();
  int randomNumber = bridgeRandomNumberGenerator.generate();
```

### 2) 람다식은 함수형 인터페이스를 구현한 인스턴스라고?

![alt](/assets/images/post/ComputerStudy/1034.png)

### 3) 남이 잘 만들어놓은 표준 함수형 인터페이스를 쓰는걸 추천해

![alt](/assets/images/post/ComputerStudy/1035.png)

#### 3-1) 표준 함수형 인터페이스를 쓰면 뭐가 좋을까요?

* 디폴트 메서드를 제공해서 다른 코드와 상호 운용성이 좋아진다.
* Predicate에서 and(),or(),negate()으로 조건을 조합해 하나의 새로운 Predicate로 결합

### 4) 메서드 참조를 하면 좀더 코드가 깔끔해질껄?

* 람다식이 하나의 메서드만 호출하는 경우에는 메서드 참조로 람다식을 간략히 할 수 있다.
* **클래스 이름 :: 메서드이름** 또는 **참조변수 :: 메서드이름**으로 바꿀수 있다.

```java
  List<String> playerNames = participants.getPlayers().stream()
            .map(player -> player.getName())
            .collect(Collectors.toList());

                    |
                    \/
  
  List<String> playerNames = participants.getPlayers().stream()
          .map(Participant:: getName)
          .collect(Collectors.toList());
```

## 출처

<a href="https://www.youtube.com/watch?v=4ZtKiSvZNu4">깃짱, 이리내의 람다와 스트림</a>