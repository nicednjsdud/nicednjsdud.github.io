---
title: Java 20. 추상클래스
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is abstract?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, abstract
last_modified_at: '2022-04-04 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

추상클래스
=========

## absract (추상적인, 미완성의)

* 클래스 앞에 붙을 때

```
   - 클래스 내에 추상 메서드가 존재하는 클래스임.
```

* 메서드 앞에 붙을 때

```
   - 선언부만 존재하고 구현부가 없는 추상 메서드임.
```

## 추상 클래스 (abstract class)

* 구현 코드없이 메서드의 선언만 있는 추상 메서드(abstract method)를 포함한 클래스
* 메서드의 선언 (declaration) : 반환타입, 메서드 이름, 매개변수로 구성
* 메서드 정의 (definition) : 메서드 구현(implemention), 구현부(body)를 가짐

```
                                  {}
           - 예) public abstract int add(int x, int y);         // 선언
           -     int add(int x, int y) {}       // 구현부가 있음. 추상메서드 아님
```

* abstract 예약어를 사용

* 추상 클래스는 new 할수 없음 (인스턴스화 할수 없음)

```
   - 모든 메서드가 구현 된 클래스라도 abstract로 선언하면 추상 클래스로 인스턴스 화 할수 없음
```

## 추상 클래스 구현하기

* 추상 클래스의 추상 메서드는 하위 클래스가 상속하여 구현

```
   - 추상 클래스 내의 추상 메서드 : 하위 클래스가 상속하여 구현 .
```

* 공통적으로 사용될 것이라고 예상되는 것을 모아서 하나의 추상클래스로 만듦.

```
   - 한곳에서 관리, 오류 줄어듦, 코드 중복 제거됨
```

## final 예약어
* final 변수 : 값이 변경될 수 없는 상수

```java
   - public static final double PI = 3.14;
```

* final 메서드 : 하위 클래스에서 재정의 할 수 없는 메서드

* final 클래스 : 상속할수 없는 클래스 

## 응용 - 템플릿 메서드 패턴
         
### 템플릿 메서드
- 추상 메서드나 구현된 메서드를 활용하여 시나리오(코드의 흐름)를 정의하는 메서드.
- final로 선언하여 하위 클래스에서 재정의(overrding) 할수 없게함.
- 프레임워크에서 많이 사용되는 설계 패턴.

* Car

```java
public abstract class Car {
	
	public abstract void drive();
	public abstract void stop();
	
	public void startCar() {
		System.out.println("시동을 켭니다.");
	}
	public void turnOff() {
		System.out.println("시동을 끕니다.");
	}
	public final void run() {
		startCar();
		drive();
		stop();
		turnOff();
	}
}
```

* ManualCar

```java
public class ManualCar extends Car{
	
	@Override
	public void drive() {
		System.out.println("사람이 운전합니다.");
		System.out.println("사람이 핸들을 조작합니다.");
	}

	@Override
	public void stop() {
		System.out.println("브레이크를 밟아서 정지합니다.");
	}
	

}
```

* SelfDrivingCar

```java
public class SelfDrivingCar extends Car{

	@Override
	public void drive() {
		System.out.println("자율 주행합니다.");
		System.out.println("차가 스스로 방향을 바꿉니다.");
	}

	@Override
	public void stop() {
		System.out.println("스스로 멈춥니다.");
	}

}
```

* Test

```java
public class CarTest {

	public static void main(String[] args) {
		
		Car manualCar = new ManualCar();
		manualCar.run();
		
		System.out.println();
		
		Car SelfDrivingCar = new SelfDrivingCar();
		SelfDrivingCar.run();
	}

}
```
