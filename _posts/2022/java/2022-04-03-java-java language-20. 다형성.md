---
title: Java 19. 다형성
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is polymorphism?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, ploymorphism
last_modified_at: '2022-04-03 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

다형성
======

## 1.다형성(polymorphism) 이란?
* 하나의 코드가 여러 자료형으로 구현되어 실행되는 것
* 같은 코드에서 여러 다른 실행 결과가 나옴
* 캡슐화(정보 은닉), 상속과 더불어 객체지향 프로그래밍의 가장 큰 특징 중 하나임.
* 다형성을 잘 활용하면 유연하고 확장서있고, 유지보수가 편리한 프로그램을 만들 수 있음.
* 하나의 참조변수 여러타입의 객체를 참조할 수 있는 것.

```
   - 하나의 코드로 여러 자료형으로 구현되어 실행되는 것
```      
      
* 상속한 클래스의 객체는 슈퍼 클래스로도 서브 클래스로도 다룰 수 있음.

```
   - 조상의 참조변수로 자손타입의 객체를 다룰 수 있는 것임.
```

* 하위클래스 객체를 상위클래스에 대입하여 사용할 수 있음.

## 2.다형성을 사용하는 이유?
* 상속과 메서드 재정의를 활용하여 확장성 있는 프로그램을 만들 수 있음.
* 그렇지 않은 경우 많은 if - else if문이 구현되고 코드의 유지보수가 어려움.
* 상위클래스에서는 공통적인 부분을 제공하고 하위 클래스에서는 각 클래스에 맞는 기능 구현.
* 여러 클래스를 하나의 타입(상위 클래스)으로 핸들링 할수 있음.

## 3.다형성으로 인한 형변환(캐스팅)
* 형변환의 전제 조건 -- 상속, 구현관계에 있는 것만 객체타입 변환이 가능.
* Up - casting : 자손타입에서 조상타입 형변환, 형변환 생략가능. 묵시적

```
   - 조작 멤버변수가 줄어듦
```

* Down - casting : 업캐스팅된 클래스를 다시 원래의 타입으로 형 변환.

```
   - 하위 클래스의 형 변환은 명시적으로 해야 함.
```

### instanceof 연산자

- 인스턴스 형 체크
- 참조변수가 참조하는 인스턴스의 실제 타입을 체크하는데 사용함.
- 원래 인스턴스의 형이 맞는지 여부를 체크해서 맞으면 true, 아니면 false 반환함.

## 4.매개변수의 다형성

* 참조타입 매개변수는 메서드 호출시, 자신과 같은 타입이거나 또는 자손타입의 주소를 인스턴스를 넘겨줌         

* Car

```java
public class Car {
		
	String color;
	int door;
	
	public void drive() {
		System.out.println("차가 달립니다.");
	}
	public void stop() {
		System.out.println("차가 멈춥니다.");
	}
}
```

* Sport Car

```java
public class SportCar extends Car {
	
	public void speedUp() {
		System.out.println("속도를 올립니다.");
	}
}
```

* Police Car

```java
public class PoliceCar extends Car {
	
	public void siren() {
		System.out.println("사이렌을 울립니다.");
	}
}
```

* CarTest

```java
public class CarTest {

	public static void main(String[] args) {
		
		Car car = null;
		SportCar sportCar=new SportCar();
		PoliceCar policeCar=new PoliceCar();
		
		sportCar.speedUp();	
		
		car = sportCar;				// 업캐스팅 (자손 -> 조상)
		
		SportCar sportCar2 = null;
		sportCar2 = (SportCar) car; // 다운캐스팅 (조상 -> 자손)
									// :조작할수 있는 멤버가 늘어남.
		sportCar2.speedUp();
		
		//sportCar = policeCar;
	}

}
```

* InstanceTest

```java
public class InstanceofTest {

	public static void main(String[] args) {
		
		SportCar sportCar = new SportCar();
		
		if(sportCar instanceof SportCar) {
			System.out.println("SportCar로 타입 변환이 가능하다.");
		}
		if(sportCar instanceof Car) {
			System.out.println("Car로 타입 변환이 가능하다.");
		}
		if(sportCar instanceof Object) {
			System.out.println("Object로 타입 변환이 가능하다.");
		}
	}

}
```
