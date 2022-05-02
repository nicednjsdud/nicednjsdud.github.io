---
title: Java 18. 상속과 오버라이딩
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is collection Inheritance and overriding?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, Inheritance, overriding
last_modified_at: '2022-04-03 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

상속과 오버라이딩
===================

## 1.상속(inheritance) 개념
* 기존의 클래스를 확장하여 새로운 클래스를 작성하는 것

### 상속하는 클래스 
- 상위 클래스, parent class, base class, super class 
- 기반 클래스, 조상 클래스

### 상속 받는클래스
- 하위 클래스, child class, derived class, subclass 
- 파생 클래스, 자손 클래스

* 자손은 조상의 모든 멤버를 상속받음 (단 생성자, 초기화 블럭 제외)
* 자손의 멤버개수가 조상보다 적을 수 없음.(같거나 많음)  

```
   - 다형성 개념 적용
   - 이미 구현된 클래스보다 더 구체적인 기능을 가진 클래스를 구현할 때 기존 클래스를 상속함.
```

```java
public class Bicycle {
	
	int id;
	String brand;
	String owner;
}
```

```java
public class MountainBike extends Bicycle{
	
	String frame;
	int gear;
	int price;
	
	public void print() {
		System.out.println("id : "+ this.id);
		System.out.println("brand : "+this.brand);
		System.out.println("frame : "+ this.frame);
		System.out.println("gear : "+ this.gear);
		System.out.println("price : "+ this.price);
		System.out.println("owner :"+this.owner);
	}

	public static void main(String[] args) {
		MountainBike mBike = new MountainBike();
		mBike.id = 824;
		mBike.brand = "LESPO";
		mBike.frame = "알루미늄";
		mBike.gear = 33;
		mBike.price= 300000;
		mBike.owner ="이순신";
		
		mBike.print();
		
	}
}
```

### 상속의 문법
- extends 키워드 뒤에 단 하나의 클래스만 올 수 있음.
- 자바는 단일 상속(single inheritance)만 지원함.

* is a 관계 : ~ 은 ~이다 (자손 클래스는 조상 클래스이다.) 

```
   - 직접적 관계  
   - 만들어질 클래스에 영향을 가장 많이 주는 클래스는 상속함.  
```

## 2.상속을 구현하는 경우

* 상위 클래스는 하위 클래스보다 더 일반적인 개념과 기능을 가짐
* 하위 클래스는 상위 클래스보다 더 구체적인 개념과 기능을 가짐
* 하위 클래스가 상위 클래스의 속성과 기능을 확장(extends)한다는 의미

## 3.포함 관계 (composite)

* 다중 상속을 대체하는 방법
* 클래스의 멤버변수로 다른 클래스를 선언하는 것
* 규모가 적은 클래스를 먼저 만들고, 이것을 조합하여 규모가 큰 클래스가 만들어감.

* has a 관계 : ~ 은 ~를 가지고 있다.  

```
   - 보조적인 것은 포함관계로 정의
```

## 4.Object 클래스

* 모든 클래스의 조상 
* 사용자 정의 클래스는 아무것도 상속을 받지 않더라도 자동으로 Object를 상속 받음.

## 5.상속에서 하위 클래스가 생성되는 과정

* 하위 클래스를 생성하면 상위 클래스가 먼저 생성됨.

```
   - new VIPCustomer()을 호출하면 Customer()가 먼저 호출됨.
```

* 클래스가 상속받은 경우 하위 클래스의 생성자에서는 반드시 상위 클래스의 생성자를 호출함.

* Customer

```java
public class Customer {

	protected int customerID;
	protected String customerName;
	protected String customerGrade;
	int bonusPoint;
	double bonusRatio;

	public Customer(int customerID, String customerName) {
		this.customerID=customerID;
		this.customerName=customerName;
		
		customerGrade = "SILVER";
		bonusRatio = 0.01;
		
		System.out.println("Customer(int, string) 생성자 호출");
		
	}
	public int calcPrice(int price) {
		bonusPoint +=price * bonusRatio;
		return price;
	}
	public int getCustomerID() {
		return customerID;
	}
	public void setCustomerID(int customerID) {
		this.customerID = customerID;
	}
	public String getCustomerName() {
		return customerName;
	}
	public void setCustomerName(String customerName) {
		this.customerName = customerName;
	}
	public String getCustomerGrade() {
		return customerGrade;
	}
	public void setCustomerGrade(String customerGrade) {
		this.customerGrade = customerGrade;
	}	
}
```

* VIPCustomer

```java
public class VIPCustomer extends Customer {

	private int agentID;
	double saleRatio;

	public VIPCustomer(int customerID,String customerName) {
		super(customerID,customerName);
		customerGrade = "VIP";
		bonusRatio= 0.05;
		saleRatio = 0.1;
		
		System.out.println("VIPCustomer() 생성자 호출");
	}

	public int getAgentID() {
		return agentID;
	}
	
	
}
```

## 6.this

* 인스턴스 자기 자신의 주소를 가지고 있는 참조변수
* 지역변수와 인스턴스 멤버변수 구별함(변수의 모호성)

## 7.super

* 하위클래스에서 가지는 상위 클래스에 대한 참조 값
* 근본적으로 this와 같음.
* 조상의 멤버와 자신의 멤버를 구별 지을 때 사용함.

## 8.super()

* 상위 클래스의 기본 생성자를 호출함
* 하위 클래스에서 명시적으로 상위 클래스의 생성자를 호춯하지 않으면 super()가 호출됨. (자동)

```
   - 이때 반드시 상위 클래스의 기본 생성자가 존재해야 함.
```

* 상위 클래스의 기본 생성자가 없는 경우 ( 다른 생성자가 있는 경우 )

```
- 하위 클래스에서는 생성자에서 super(x)를 이용하여 명시적으로 상위 클래스의 생성자를 호출 함.
```

## 9.오버라이딩 (Overiding) -- 재정의

* 조상클래스에서 상속받은 메서드를 자손한테 맞게끔 구현부를 수정하는 것.
* 반드시 메서드 선언부는 동일해야 함 (리턴타입, 메서드명, 매개변수)
* modify, change의 개념 

## 10.오버로딩 (Overloading)

* 매개변수의 갯수, 타입, 순서가 다른 경우임.

```
     매개변수의 이름과 리턴타입은 영향을 주지 않음.
```

* 새로운 메서드를 만드는 것 (new의 개념)
     


