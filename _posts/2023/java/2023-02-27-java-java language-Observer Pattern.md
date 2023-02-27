---
published: true
title: Java 44. Observer Pattern (Design Pattern - 13s)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Observer Pattern (Design Pattern - 13)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Observer Pattern

## 1. Observer Pattern 이란?

- 객체사이에 일대다의 의존 관계가 있고, 어떤 객체의 상태가 변하게 되면 그 객체에 의존성을 가진 다른 객체들이 변화의 통지를 받고  
  자동으로 갱신될 수 있게 함
- dependent, publish-subscribe

## 2. 의도와 동기

- 하나의 객체에 연동되는 여러 객체 집합이 있을 때 변화에 대한 일관성을 유지하고, 객체간의 결합도는 낮게하기 위한 패턴
- 변화에 관심이 있는 객체에 대한 가정없이 통보 될 수 있도록 해야 함
- 주로 data-view의 관계에서 사용됨
- log와 그 handler들의 관계. (file, console 등등)

## 3. 객체 협력

### 1) Subject

- Observer를 알고 있는 주체, Observer를 더하거나 뺄 수 있음

### 2) Observer

- Subject의 변화에 관심을 가지는 객체
- 갱신에 필요한 인터페이스 정의, 객체들의 일관성을 유지

### 3) ConcreteSubject

- ConcreteObserver에게 알려주어야하는 상태가 변경될때 통보
- 주로 List로 Observer 관리

### 4) ConcreteObserver

- 객체에 대한 참조자를 관리하함
- Subject의 일관성 유지
- Subject가 변경될 때 갱신되는 인터페이스 구현

## 4. 중요한 결론

- Subject와 Observer간의 추상적인 결합만의 존재
- BroadCast 방식의 교류가 가능
- 데이타와 그 뷰 사이에 자주 사용되는 방법

## 5. 예제

- observer.java (interface)

```java
  package observer;

  public interface Observer{

    public void update(NumberGenerator generator);

  }
```

- NumberGenerator.jaba

```java
  package observer;

  public abstract class NumberGenerator {

    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer){
      observers.add(observer);
    }

    public void removeObserver(Observer observer){
      observers.remove(observer);
    }

    public void notifyObservers(){
      Iterator<Observer> ir = observers.iterator();

      while(ir.hasNext()){
        Observer observer = ir.next();
        observer.update(this);
      }
    }

    public abstract int getNumeber();
    public abstract void excute();
  }
```

- GraphObserver.java

```java
  package observer;

  public class GraphObserver implements Observer {

    @Override
    public void update(NumberGenerator generator){

      System.out.println("GraphObserver");
      int number = generator.getNumber();

      for(int i = 0; i< number; i ++){
        System.out.print("*");
      }
      System.out.println();

      try{
        Thread.sleep(100);
      }catch(InterruptedException e){
        e.printStackTrace();
      }
    }
  }
```

- DigitObserver.java

```java
  package observer;

  public class DigitObserver implements Observer {

    public void update(NumberGenerator generator){
      systm.out.println("DigitObserver: " + generator.getNumber());
      try{
        Thread.sleep(100);
      } catch(InterruptedException e){
        e.printStackTrace();
      }
    }
  }
```

- RandomNumberGenerator.java

```java
  package observer;
  public class RandomNumberGenerator extends NumberGenerator{

    private int number;
    private Random random = new Random();

    @Override
    public int getNumber(){
      return number;
    }

    @Override
    public void excute(){
      for(int i = 0 ; i < 50; i ++){
        number = random.nextInt(50);
      }
    }
  }
```

- Main.java

```java
  package observer;

  public class Main {

    public static void main(String[] args){

      NumberGenerator generator = new RandomNumberGenerator();
      Observer observer1 = new DigitObserver();
      Observer observer2 = new GraphObserver();
      generator.addObserver(observer1);
      generator.addObserver(observer2);
      generator.execute();
    }
  }
```
