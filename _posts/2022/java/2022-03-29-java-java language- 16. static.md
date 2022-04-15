---
title: Java 14. static
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is static?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java static
last_modified_at: '2022-03-29 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Static
===========

## 1.static 변수

### 1) 공통으로 사용하는 변수가 필요한 경우

* 여러 인스턴스가 공유하는 기준 값이 필요한 경우

```
   - 학생마다 새로운 학번 생성
   - 카드회사에서 카드를 새로 발급할 때마다 새로운 카드 부여 
   - 회사에 사원이 입사할 때 마다 새로운 사번이 필요한 경우
```

```java
public class Card {
	
	// 인스턴스 변수 -- 인스턴스 생성해야 접근 가능
	private String color;
	private String company;
	
	static int width =100;
	static int height = 50;
	
	public String getColor() {
		return color;
	}
	public void setColor(String color) {
		this.color = color;
	}
	public String getCompany() {
		return company;
	}
	public void setCompany(String company) {
		this.company = company;
	}
	
```

```java
public class CardTest {

	public static void main(String[] args) {
			
		Card card = new Card();
		card.setColor("노랑");
		card.setCompany("KB은행");
		System.out.println(card);
		
		Card.height =150;
		Card.width=80;
		Card card2=new Card();
		card2.setColor("파랑");
		card2.setCompany("농협");
		System.out.println(card2);
		
		
	}

}
```


### 2) static int serialNum;        

* 인스턴스가 생설될 때 만들어지는 (인스턴스)변수가 아닌,   
  처음 프로그램이 메모리에 로딩될 때 메모리를 할당.
* 클래스 변수, 정적변수 라고도 함 
* 인스턴스 생성과 상관 없이 사용 가능
* 클래스이름.클래스변수

```java
   - 클래스 이름으로 직접 참조
   public static int serialNum = 1000;
```

## 2.static 메서드 

* 클래스 메서드, 정적 메서드
* 인스턴스 생성과 무관하게 클래스 이름으로 호출 될 수 있음.
* 인스턴스 생성전에 호출 될수 있음.

```
  - static 메서드 내부에서는 인스턴스 변수를 사용할 수 없다.
```

```java
public class MyCalculator {
	
	public static int adder(int num1,int num2) {
		return num1 + num2;
	}
	
}
```

```java
public class UtilityMethod {

	public static void main(String[] args) {
		MyCalculator calculator1 = new MyCalculator();
		int num1 = calculator1.adder(1, 2);
		System.out.println(num1);
		
		// 객체를 생성하지 않고 사용 (권장)
		int num2 = MyCalculator.adder(2,3);			//클래스명.메서드명
		System.out.println(num2);
	}
	

}
```

## 3.static (초기화) 블록

* 스태틱 예약어로 지정된 영역이 프로그램 실행전 메모리에 먼저 로드가 되고 실행이 됨.

## 4.변수의 유효 범위와 메모리

```
   변수 유형         선언위치             사용 범위               메모리
   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   지역 변수         함수 내부에 선언     함수 내부에             스택
   (로컬 변수)                           서만 사용

   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   멤버 변수         클래스 멤버     - 클래스 내부에서 사용       
   (인스턴스 변수)    변수로 선언    - private이 아니면 다른       힙
                                      클래스에서 사용 가능
   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   static 변수       static 사용해        (위와 동일)       
   (클래스 변수)     클래스 내부에 선언                           데이터 영역

```
```

   변수 유형               생성 과 소멸
   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   지역변수        - 함수가 호출 될때 생성되고
   (로컬 변수)     - 함수가 끝나면 소멸함

   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   멤버변수        - 인스턴스가 생성될 때 heap에 생성되고,
   (인스턴스 변수) - 가비지 컬렉터(GC)가 메모리를 수거할때 소멸됨    

   ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
   static 변수     - 프로그램이 처음 시작할 때 상수와 함께
   (클래스 변수)      데이터영역에 생성되고
                   - 프로그램이 끝나면 메모리를 해제할때 소멸
```

## 5.static 응용 - 싱글톤 패턴 (singleton pattern)

## 1) 싱글톤 패턴이란?

* 프로그램에서 인스턴스가 단 한 개만 생성되어야 하는 경우 사용하는 디자인 패턴
* static 변수, 메서드를 활용하여 구현 할수 있음.

## 2) 싱글톤을 사용하는 경우

* 사용자 환경설정, 시각, 날짜 정보, 커넥션 풀

```
   - 단 하나의 인스턴스만 생성하고 그걸 사용하면 됨
```

## 3) 싱글톤 패턴으로 구현하기

* 생성자는 private으로 선언 
* 클래스 내부에 유일한 private 인스턴스 생성
* 외부에서 유일한 인스턴스를 참조할 수 있도록 public 메서드 제공

```java
public class Company {
	
	private Company() {}
	private static Company instance = new Company();
	public static Company getInstance() {
		if(instance == null) {
			instance = new Company();
		}
		return instance;
	}
	
}
```


