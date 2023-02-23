---
published: true
title: Java 41. 동일시하기와 위임하기 Decorator (Design Pattern - 9)
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
last_modified_at: "2023-02-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 동일시하기와 위임하기 Decorator,Composite

## 1. Decorator Pattern 이란?

- 장식과 실제 내용물을 동일시
- 객체에 동적으로 책임을 추가

## 2. 의도와 동기

- 상속을 사용하지 않고 기능의 유연한 확장이 가능한 패턴
- 객체에 동적으로 새로운 서비스를 추가 할 수 있음
- 전체가 아닌 개별적인 객체에 새로운 기능을 추가할 수 있음

## 3. 객체 협력

### 1) Component

- 동적으로 추가할 서비스를 가질 수 있는 객체 정의

### 2) ConcreteComponent

- 추가적인 서비스가 필요한 실제 객체

### 3) Decorator

- Component 참조과를 관리하면서 Component에 정의된 인터페이스를 만족하도록 정의

### 4) ConcreteDecorator

- 새롭게 추가되는 서비스를 실제 구현한 클래스로 addBehavior()를 구현

## 4. 중요한 결론

- 단순한 상속보다 설계의 융통성을 증대
- Decorator의 조합을 통해 새로운 서비스를 지속적으로 추가할 수 있음
- 필요없는 경우 Decorator를 삭제할 수 있음
- Decorator와 실제 컴포넌트는 동일한 것이 아님
- 작은 규모의 객체들이 많이 생성될 수 잇음
- 자바의 I/O 스트림 클래스는 Decorator 패턴임

## 5. 예제

- Coffee.java

```java
  package coffee;

  public abstract class Coffee{

    public abstract void brewing();
  }
```

- EtopiaCoffe.java

```java
  package coffee;

  public class EtiopiaCoffe extends Coffee{

      @Override
      public void brewing(){
        System.out.println("EtipoiaAmericano");
      }
  }
```

- KeyaCoffee.java

```java
  package coffee;

  public class KeyaCoffee extends Coffee{

      @Override
      public void brewing(){
        System.out.println("KeyaCoffeeAmericano");
      }
  }
```

- Decorator.java

```java
  package coffee;

  public class Decorator extends Coffee{

      Coffee coffee;

      public Decorator(Coffee coffee){
        this.coffee = coffee;
      }

      @Override
      public void brewing(){

        coffee.brewing();
      }
  }
```

- Latte.java

```java
  package coffee;

  public class Latte extends Decorator{

    public Latte(Coffee coffee){
      super(coffee);
    }

       @Override
      public void brewing(){

        coffee.brewing();
        System.out.println("Adding Milk");
      }
  }
```

- MochaCoffee.java

```java
  package coffee;

  public class MochaCoffee extends Decorator{

      public Latte(Coffee coffee){
      super(coffee);
    }

       @Override
      public void brewing(){

        coffee.brewing();
        System.out.println("Adding Mocha Syrup");
      }
  }
```

### 1) Test

- CoffeTest.java

```java
  package coffee;

  public class CoffeeTest {

      public static void main(String[] args){

        Coffee keyaCoffee = new KeyaCoffee();
        keyaCoffe.brewing();    // KeyaAmericano

        Coffee keyaLatte = new Latte(keyaCoffee);
        keyaLatte.brewing();    // keyaAmericano Adding Milk

        Coffee mochaKeya = new MochaCoffe(new Latte(new KeyaCoffee()));
        mochaKeya.brewing();    // keyaAmericano Adding Milk Adding Mocha syrup

        Coffee etipoiaCoffe = new MochaCoffee(new Latte(new EtiopiaCoffee));
        etipoiaCoffe.brewing(); // EtiopiaAmericano Adding Milk Adding Mocha syrup
      }
  }
```
