---
published: true
title: Java 38. Factory Method Pattern (Design Pattern - 6)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Factory Method Pattern
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-22 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Factory Method Pattern

## 1. Factory Method Pattern 이란?

- 인스턴스 작성을 하위 클래스에게 위임
- Template Method 패턴을 인스턴스 생성에 적용

## 2. 의도와 동기

- 객체를 생성하기 위한 인터페이스를 정의하지만, 어떤 클래스의 인스턴스를 생성할지에 대한 결정은 서브클래스에서 결정하게 함.
- 여러 상황에 따라 각각 생성될 수 있는 객체에 대한 생성을 하위 클래스에 위임
- 생성과 관련된 동일한 메서드는 상위 클래스에서 처리

## 3. 객체 협력

-

## 4. 중요한 결론

- 상황에 따라 다양한 인스턴스 생성을 할 수 있음

## 5. 예제

- Car.java

```java
package factorymethod;

public abstract class Car {

  String carType;

  public String toString(){
    return carType;
  }
}
```

- Sonata.java

```java
  package factorymethod;

  public class Sonata {

     public Sonata(){
    cartype = "Sonata"
  }
  }
```

- Santafe.java

```java
package factorymethod;

public class Santafe {

  public Santafe(){
    cartype = "Santafe"
  }

}
```

- CarFactory.java

```java
package factroymethod;

public abstract class CarFactory {

    public abstract Car createCar(String name);

    public abstract Car returnCar(String name);

    public void numbering(){
      System.out.println("numbering");
    }

    public void washCar(){
      System.out.println("washCar");
    }

    final public void sellCar(String name){

        numbering();
        createCar(name);
        washCar();
    }
}
```

- HyundaiCarFactory.java

```java
package factorymethod;

public class HyundaiCarFactory extends CarFactory {

    HashMap<String, Car> carMap = new HashMap<String, Car>();

    @Override
    public Car createCar(String name){
      Car car = null;

      if( name == "sonata"){
        car = new Sonata();
      }
      else if( name == "santafe"){
        car = new Santafe();
      }
      return car;
    }

    @Override
    public Car returnCar(String name){

      Car car = carMap.get(name);

      if(car == null){

          if(name.equals("Tomas")){
              car = new Sonata();
          }
          else if(name.equals("James")){
              car = new Santafe();
          }
          carMap.put(name, car);
      }
      return car;
    }
}
```

- CarTest.java

```java
package factorymethod;

public class CarTest {

  public static void main(String[] args){

    CarFactory factory = new HyundaiCarFactory();
    Car newCar = factory.crateCar("sonata");

    System.out.println(newCar);   // sonata

    Car myCar = factory.returnCar("Tomas"); // Sonata
    Car hisCar = factory.returnCar("Tomas");  // Sonata
  }
}
```
