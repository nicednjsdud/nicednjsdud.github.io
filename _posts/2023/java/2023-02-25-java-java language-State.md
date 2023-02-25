---
published: true
title: Java 44. State Pattern (Design Pattern - 12)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: State Pattern (Design Pattern - 12)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-25 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# State Pattern

## 1. State Pattern 이란?

- 클래스가 하나의 상태에 따라 그 내부의 여러 메서드의 기능이 바뀐다고 하면 이를 각각의 클래스로 분리

## 2. 의도와 동기

- 객체의 기능은 상태에 따라 달라질 수 있는데, 이러한 상태가 여러가지이고, 클래스 전반의 모든 기능이 상태에 의존적이라 하면, 상태를  
  클래스로 표현하는것이 적절함
- 클래스로 분리하지 않게 되면 상태가 여러가지인 경우 많은 if-else문이 사용되고 추후 상태가 추가되거나 삭제될 때 수정해야 하는 사항이 너무 많아짐

## 3. 객체 협력

### 1) Context

- ConcreteState의 인스턴스를 관리하고 서로 상태가 바뀌는 순간을 구현할 수 있다.

### 2) State

- Context가 사용할 메서드를 선언한다.

### 3) ConcreteState

- 각 상태 클래스가 수행할 State에 선언된 메서드를 구현

## 4. 중요할 결론

- 상태에 다른 기능을 분리하여 구현
- 새로운 상태가 추가되면 새로운 클래스를 추가한다.
- 각 상태의 switch를 명확하게 구현해야 함

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

  //   final public void go(int count){

  //   }
  // }
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
        level = new BignnerLevel();
        level.showLevelMessage();
    }

    public void upgradeLevel(){
      this.level = level;
      level.showLevelMessage();
    }

    public PlayerLevel getPlayerLevel(){
      return level;
    }

    public void play(int count){
      run();
      for(int i = 0; i < count; i++){
        jump();
      }
      turn();
    }
    public void run(){
      level.run();
    }
    public void jump(){
      level.jump();
    }
    public void turn(){
      level.turn();
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

      level = new AdvancedLevel();
      player.upgradeLevel(level);
      player.play(2);  // 중급자 레벨

      level = new SuperLevel();
      player.upgradeLevel(level);

      player.play(5);  // 상급자 레벨

    }
  }
```
