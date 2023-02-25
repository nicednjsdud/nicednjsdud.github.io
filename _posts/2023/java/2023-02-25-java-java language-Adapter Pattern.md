---
published: true
title: Java 43. Adapter Pattern (Design Pattern - 11)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: 동일시하기와 위임하기 Decorator,Composite
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-25 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Adapter Pattern

## 1. Adapter Pattern이란?

- 서로 다른 인터페이스를 중간에서 연결해주는 기능
- 이미 사용중이거나 정의된 인터페이스들을 중간에서 맞춰서 적용해 줄 수 있음
- 예 ) 안드로이드 ListView Adpter

## 2. 의도와 동기

- 클라이언트에서 사용하던 방식대로 호출하여 사용할 수 있도록 조정해주는 기능
- 서로 일치하지 않는 인터페이스를 변경하지 않고 중간에서 호출하여 사용할 수 있도록 제공
- Wrapper

## 3. 해결 방법

- 상속을 활용하여 구현하는 Adapter
- 객체 합성의 방법으로 구현하는 Adapter

## 4. 객체 협력

### 1) Target

- 클라이언트가 사용할 인터페이스를 정의하고 있는 클래스

### 2) Clinet

- Target 인터페이스를 사용하는 객체

### 3) Adaptee

- 실제의 새롭거나 적용될 기능이 제공되는 클래스

### 4) Adapter

- Target 인터페이스에 Adaptee의 인터페이스를 맞춰주는 클래스

## 5. 중요한 결론

- Adapter를 사용함으로써 클라이언트가 사용하는 방식은 동일하면서 여러 기능이 제공 될 수 있다.
- 예를 들어 안드로이드에서는 여러 View를 구현할 때 이에 대한 item들을 직접 View에 올리지 않고, Adapter를 이용하여 Adapter에서  
  item을 관리하고 그리는 방식을 정하도록 한다.
- 이 방법은 실제 보여주는 부분과 데이터가 다양한 방식의 View에 활용될 수 있고, 이 때 중간에서 사용되는 여러 Adapter등이 데이터와  
  View를 연결해준다.

## 6. 예제

- Print.java (interface)

```java
  package adapter;
  public interface Print {

    public void printWeek();
    public void printStrong();
  }
```

- Banner.java

```java
  package adapter;
  public class Banner{

    private String string;
    public Banner(String string){
      this.string = string;
    }

    public void showWithParen(){

      System.out.println("(" + string + ")");
    }

    public void showWithAster(){

      System.out.println("**" + string + "**");
    }
  }
```

- PrintBanner.java

```java

  package adapter;

  public class PrintBanner implements Print  {

    private Banner banner;

    public PrintBanner(String string){
      banner = new Banner(string);
    }

    @Override
    public void printWeek(){
      banner.showWithParen();
    }

    @Override
    public void printString(){
      banner.showWithAster();
    }
  }
```

- Main.java

```java
  package adpater;

  public class Main {

    public static void main(String[] args){

      Print print = new PrintBanner("hello");
      print.printStrong();    // **hello**
      print.printWeek();      // (hello)
    }
  }
```
