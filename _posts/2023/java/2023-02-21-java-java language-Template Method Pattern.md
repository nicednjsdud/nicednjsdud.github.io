---
published: true
title: Java 37. Template Pattern (Design Pattern - 5)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Template Pattern
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Template Pattern

## 1. Template Method Pattern 이란?

- 상위 클래스에서는 전체적인 흐름을 구현하고 구체적인 처리는 하위 클래스에 위임

## 2. 의도와 동기

- Operation에 알고리즘의 기본 골격 주고를 정의하고 구체적인 단계는 서브클래스에 정의
- 추상화된 함수를 통해서 알고리즘의 일부 단계를 정의함으로써 템플릿 메서드의 처리순서를 정할 수 있음

## 3. 객체 협력

### 1) AbstractClass

- 서브 클래스들이 반드시 구현해야 하는 알고리즘 처리 단계 내의 기본 오퍼레이션이 무엇인지를 정의한다.
- 서브 클래스에서 이들 오퍼레이션들을 구현함

### 2) ConcreteClass

- 상위 클래스에서 선언된 추상 메서드를 구현하거나 이미 구현된 메서드를 재정의

## 4. 중요한 결론

- 템플릿 메서드는 코드 재사용을 위한 기본 기술
- 프레임워크에서 가장 많이 사용되는 패턴 중 하나
- 클래스의 공통부분을 분리하는 기능 제공

### 1) 템플릿 메서드에서 사용하는 오퍼레이션들

- ConcreteClass 오퍼레이션이나 클라이언트 클래스에 정의된 오퍼레이션
- AbstractClass 에 정의된 오퍼레이션 중 구체적인 알고리즘을 가지고 있는 오퍼레이션
- 기본 오퍼레이션으로 추상화된 오퍼레이션
- 훅 오퍼레이션

## 5. 예제

- PlayerLevel.java

```java
  package gamelevel;

  public abstract class PlayerLevel {

    public abstract void run();
    public abstract void jump();
    public abstract void turn();
    public abstract void showLevelMessage();

    public void fly(){} // 훅 메서드 (하위클래스에 반드시 들어가야 하는 것이 아님)

    final public void go(int count){
      run();
      for(int i = 0; i < count; i++){
        jump();
      }
      turn();

      fly();
    }
  }
```

- BeginnerLevel.java

```java
  package gamelevel;

  public class BeginnerLevel extends PlayerLevel {

    @Override
    public void run(){
      System.out.println("천천히 달립니다.");
    }

    @Override
    public void jump(){
      System.out.println("Jump 할 줄 모릅니다.");
    }

    @Override
    public void turn(){
      System.out.println("Turn 할 줄 모릅니다.");
    }

    @Override
    public void showLevelMessage(){
      System.out.println("초보자 레벨 입니다.");
    }
  }
```

- AdvancedLevel.java

```java
package gamelevel;

  public class AdvancedLevel extends PlayerLevel {

    @Override
    public void run(){
      System.out.println("빨리 달립니다.");
    }

    @Override
    public void jump(){
      System.out.println("높이 Jump 합니다.");
    }

    @Override
    public void turn(){
      System.out.println("Turn 할 줄 모릅니다.");
    }

    @Override
    public void showLevelMessage(){
      System.out.println("중급자 레벨 입니다.");
    }
  }
```

- SuperLevel.java

```java
package gamelevel;

  public class SuperLevel extends PlayerLevel {

    @Override
    public void run(){
      System.out.println("아주 빨리 달립니다.");
    }

    @Override
    public void jump(){
      System.out.println("아주 높이 Jump 합니다.");
    }

    @Override
    public void turn(){
      System.out.println("한바퀴 돕니다..");
    }

    @Override
    public void showLevelMessage(){
      System.out.println("고급자 레벨 입니다.");
    }
  }
```

- Player.java

```java
  package gamelevel;

  public class Player {

    private PlayerLevel level;

    public Player(){

        level = new BeginnerLevel();
        level.showLevelMessage();
    }

    public void upgradeLevel(PlayerLevel level){
      this.level = level;
    }

    public PlayerLevel getPlayerLevel(){
      return level;
    }

    public void play(int count){
      level.go(count);
    }
  }
```

- MainBoard.java

```java
  package gamelevel;

  public class MainBoard {

    public static void main(String[] args){

      Player player = new Player();

      player.play(1);    // 초보자 레벨

      PlayerLevel level = new AdvancedLevel();
      player.upgradeLevel(level);

      player.play(2);  // 중급자 레벨

      level = new SuperLevel();
      player.upgradeLevel(level);

      player.play(5);  // 상급자 레벨

    }
  }
```
