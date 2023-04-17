---
published: true
title: (10분 테크톡) Java 56. OOP
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
last_modified_at: "2023-04-16 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# OOP

## 목차

1. 객체지향 프로그래밍이란?
2. 키워드로 알아보는 객체지향
3. 객체지향적인 치킨집 만들기

## 1. 객체지향 프로그래밍이란?

1. 프로그래밍 개발 방법론
2. 사람이 현실을 바라보는 방법을 개발에 접목

- 직관적으로 이해하기 쉽다.
- 유지 보수를 용이하게 만든다.

## 2. 키워드로 알아보는 객체지향

1. 객체
2. 협력과 책임, 역할
3. 메시지
4. 자율성 (의인화)
5. 다형성

### 1) 객체란 무엇인가?

- 객체는 현실의 무언가에 대응하는 개념이다.
- class는 객체를 표현하는 하나의 수단이다. (class != 객체)
- 다른 객체와 **협력**하는 **역할**을 맡고 있는 대상
- **역할**을 맡으면 임무를 수행할 **책임**이 생긴다.
- 책임을 다하기 위한 데이터와 프로세스를 가지고 있다.

### 2) 협력과 책임, 역할

#### 2-1) 협력 이란?

- 시스템 목표를 달성하기 위해 여러 객체가 참여하여 행동하는 것
- ex) 치킨을 튀겨서 손님에게 배달해야 한다.

#### 2-2) 책임 이란?

- 협력 속에서 본인이 수행해야 할 임무의 내용을 알고, 수행하는 것
- ex) 치킨을 튀길 객체는 치킨을 맛있게 조리할 책일을 갖는다.

#### 2-3) 역할 이란?

- 동일한 목적을 가진 책임의 묶음
- ex) 치킨을 조리할 책임을 가지는 역할은 요리사이다.

#### 2-4) 다시보기

- **협력**이란 문제 상황을 해결하기 위해 여러 객체가 참여하여 행동하는 것이다.
- **역할**을 맡으면 임무를 수행할 **책임**이 생긴다.
- 치킨을 손님에게 배달하기 라는 **협력**을 완수하기 위해, **치킨 가게 객체**는 치킨을 튀기는 **책임(역할)**을 수행하고  
  **배달원 객체**는 손님에게 치킨을 전달하는 **책임(역할)**을 수행한다.

![alt](/assets/images/post/ComputerStudy/947.png)

### 3) 메시지

- 객체는 **메시지**를 통해 다른 객체에 **책임**을 다하라고 요구한다.
- 메시지를 보내는 객체는 **무엇을** 할지만 요구하고, **어떻게** 하는지는 신경쓰지 않아도 된다.
- 객체는 **책임**을 수행하라고 요구받지만, 어떻게 처리할 지는 **자율**에 맡긴다.

![alt](/assets/images/post/ComputerStudy/948.png)

```java
// 자바에선 메소드를 호출함으로써 메시지를 보낸다.
class ChickenShop {

  public void cookChicken(){  // 메소드 이름과 리턴 타입은 메시지를 표현한다.

      ...   // 치킨을 요리하라는 메시지를 받아 요리를 시작
            // 나는 나만의 요리를 해
  }

  public void deliverChicken(){

      ...   // 치킨을 다른 객체에게 전달한다.
  }
}
```

### 4) 자율성 (의인화)

- 객체지향과 현실세계의 차이점

  - 현실 세계의 치킨 가게는 건물에 불가하다.
  - 객체지향 세계의 치킨 가게는 스스로 치킨을 튀기고, 치킨을 건네어 준다.

- 즉, 객체지향에선 객체가 자율적으로, 능동적으로 행동할 수 있다고 **의인화** 하여야 한다.
- 자율적으로 메시지를 처리하기 위해서 자신의 책임을 수행하는 데 필요한 데이터와 프로세스를 가지고 있다.

```java
class ChickenShop {

  public void cookChicken(){

      ...   // 스스로 치킨을 튀긴다.
  }

  public void deliverChicken(){

      ...   // 치킨을 다른 객체에게 전달한다.
  }
}
```

### 5) 다형성

- 다형성을 활용하는 목적은 서로 다른 유형의 객체가 동일한 메시지에 대해 다르게 반응하게 하기 위해서이다.
- 동일한 메시지를 처리한다 == 같은 역할을 수행한다.
- 다르게 반응하다. == 메시지 처리방 법은 자율적이다.

```java
// ChickenShop과 같은 역할과 책임을 수행할 수 있다.
class ElectricChickenShop extends chickenShop {

  public void cookChicken(){

        ...   // 똑같이 치킨을 요리하지만 어떤 치킨을 튀길지는 자율이다.
  }

  public chicken getChicken(){

        ...   // 전기구이 통닭을 리턴한다.
  }
}
```

### 6) 세줄 정리

1. 객체는 현실의 개념을 추상화한 것이다.
2. 객체들은 서로 협력하고, 역할을 맡아 책임을 수행하여 문제상황을 해결한다.
3. 하지만 현실의 사물과 달리 객체는 능동적이고 자율적인 존재이다.

## 3. 객체지향적으로 설계해보기

### 1) 빠지기 쉬운 함정

- 현실 세계를 반영하기 위한 설계를 시작하면 자칫 데이터 중심의 설계를 하기 쉽다.
- 치킨집은 요리사, 전화기를 가지고 있어야해. 배달원은 배달 도착지, 치킨, 받아야 할 돈을 가지고 있어야하고....

```java
class ChikcenShop{

    private Chef chef = new Chef();
    private Phone phone = new Phone();

    private void processChickenOrder(){

      Memnu orderMenu = phon.getMenu();
      List<Menu> possibleMenuList = chef.getMenuList();

      Driver driver = new Driver();
      if(possibleMenuList.contains(orderMenu)){

        Chicken chicken = chef.cook(orderMenu);
        driver.setChicken(chicken);
        driver.setDestination(order.getDetination());
        driver.deliver();
      }
    }
}
```

#### 1-1) 데이터 중심의 설계의 문제점 - 1

- getter, setter가 과도하게 추가되어 결합도가 높아진다. (서로 알고 있는 객체가 많아진다.)

#### 1-2) 데이터 중심의 설계의 문제점 - 2

- 데이터를 처리하는 작업과 데이터가 분리되어 응집도가 낮아진다. (여러가지 이유로 변경되어야 한다.)

### 2) 책임 주도 개발

1. 시스템이 사용자에게 제공해야 하는 기능인 시스템 책임을 파악한다.
2. 시스템 책임을 더 작은 책임으로 분할한다.
3. 분할된 책임을 수행할 수 있는 적절한 객체 또는 역할을 찾아 책임을 할당한다.
4. 객체가 책임을 수행하는 도중 다른 객체의 도움이 필요한 경우 이를 책임질 적절한 객체 또는 역할을 찾는다.
5. 해당 객체 또는 역할에게 책임을 할당함으로써 두 개게가 협력하게 한다.

#### 2-1)

1. 시스템이 사용자에게 제공해야 하는 기능인 시스템 책임을 파악한다.

- 치킨 주문을 받아 손님에게 배달해야 한다.

#### 2-2)

2. 시스템 책임을 더 작은 책임으로 분할한다.

- 메세지를 생성한다.
  - 치킨 주문을 받는다.
  - 치킨을 요리한다.
  - 치킨을 손님에게 배달한다.

#### 2-3)

3. 분할된 책임을 수행 할 수 있는 적절한 객체 또는 역할을 찾아 책임을 할당한다.

![alt](/assets/images/post/ComputerStudy/949.png)

#### 2-4)

4. 객체가 책임을 수행하는 도중 다른 객체의 도움이 필요한 경우 이를 책임질 적절한 객체 또는 역할을 찾는다.

![alt](/assets/images/post/ComputerStudy/950.png)

#### 2-5)

5. 해당 겍체 또는 역할에게 책임을 할당함으로써 두 객체가 협력하게 된다.

```java
  class ChickenShop{

    private Chef chef = new Chef();

    public void takeOrder(){
      chef.cook();
    }
  }
```

![alt](/assets/images/post/ComputerStudy/951.png)

```java
  class Chef{

    private Driver driver = new Driver();
    private Chicken chicken;

    public void Cook() {

      chicken = new FriedChicken();   // 고추 바사삭 순살
      driver.deliver(chicken);
    }
  }
```

```java
  class Driver {

    public void deliver(Chicken chicken){
      ...
    }
  }
```

![alt](/assets/images/post/ComputerStudy/952.png)

## 출처

<a href="https://www.youtube.com/watch?v=3etKkkna-f0">웨지의 OOP</a>
