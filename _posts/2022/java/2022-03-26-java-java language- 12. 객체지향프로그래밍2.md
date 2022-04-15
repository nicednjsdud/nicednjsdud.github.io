---
title: Java 10. 객체지향프로그래밍 2
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is 객체지향프로그래밍?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language,
last_modified_at: '2022-03-26 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

객체지향프로그래밍
=================

## 1. 클래스와 객체

* 객체는 클래스에서 정의된 내용대로 메모리에 생성된 것을 의미함.

* 객체(Object)나 인스턴스 (instance)는 같은 말로 생각하면 됨.

```
    - 객체는 인스턴스를 포함하는 형태임.
    - instantiate, 인스턴스화 
    - class로부터 instance를 생성하는 것.
```

* 클래스의 구성요소

```
    - 속성(멤버변수)
    - 기능(멤버 메서드)
```

* 인스턴스 생성

```
        클래스명 참조변수명 = new 클래스명();
```

* this : 객체 자기자신의 주소
* super : 조상객체의 주소

```java
class A{
	int value;
}

class B{
	int value;
	
//	public B() {}
	public B(int value) {
		this.value=value;
	}
}
public class ConstructorTest {

	public static void main(String[] args) {
		A a= new A();
		
		B b= new B(20);
		System.out.println(a);
		System.out.println(b);
	}

}
```

## 2. 접근 제한자, 접근 제어 지시자(access modifier) & 정보은닉 (infomation, hiding)

* 변수나 메서드에 접근 제한자를 지정하면 접근을 제한 할수 있음

* 클래스 외부에서 클래스의 멤버변수, 메섣, 생성사를 사용할 수 있는지 여부를 지정하는
       
### 키워드

```
    - public : 외부 클래스 어디에서나 접근 가능함
    - protected : 같은 패키지 내부와 상속 관계의 클래스에서만 접근 가능함.
    - (아무것도 표시안 함, default) : 같은 패키지 내부에서만 접근 가능함.
    - private : 
        - 같은 클래스 내부에서만 접근 가능함.
        - 외부 클래스, 상속관계의 클래스에서도 접근 불가.
```

### get()/set() 메서드

* private으로 선언된 멤버 변수(필드)에 대해 접근, 수정할수 있는 메서드를 public 으로 제공

* get() 메서드만 제공되는 경우 => read-only 필드         

## 3. 함수와 메서드

### 1) 함수(function)

- 하나의 기능을 수행하는 일련의 코드
- 구현된(정의된) 함수는 호출하여 사용하고 호출된 함수는 기능이 끝나면 제어가 반환
- 함수로 구현된 하나의 기능은 여러 곳에서 동일한 방식으로 호출되어 사용될 수 있음.
    
### 2) 함수 호출(Call Stack)과 스택 메모리 
- 메서드의 작업공간
- 스택(stack) : 함수가 호출될 때 지역 변수들이 사용하는 메모리
- 함수의 수행이 끝나면 자동으로 반환되는 메모리 

### 3) 메서드 (method)

- 객체의 기능을 구현하기 위해 클래스 내부에 구현되는 함수

- 멤버 함수(member function) 이라고도함
- 메서드를 구현함으로써 객체의 기능이 구현됨
- 메서드의 이름은 그 객체를 사용하는 객체에 맞게 짓는것이 좋음.
        
## 4. 인스턴스 생성과 힙 메모리 (heap memory)

### 1) 인스턴스(instance)

- 클래스는 객체의 속성을 정의하고, 기능을 구현하여 만들어 놓은 코드 상태

- 실제 클래스 기반으로 생성된 객체(인스턴스)는 각각 다른 멤버변수 값을 가지게됨

```
- ex) 학생의 클래스에서 생성된 각각의 인스턴스는 각각 다른 이름, 학번,학년 등의 값을 가지게 됨.
```

- new 키워드를 사용하여 인스턴스의 생성

### 2) 힙 메모리 
- 생성된 인스턴스는 동적 메모리(heap memory)에 할당이 된다.
            
### 3) JVM 메모리 모델

```
                메서드 영역              스택영역(call stack)            힙영역        

                ---------------
                프로그램 실행코드
                                                                        객체 1      

                ---------------         ------------------
                                        power() 지역변수
                static 영역                      매개변수                객체 2
                ---------------         -------------------
                상수 pool                main() 지역변수
                                                매개변수                객체 3
                ---------------------------------------------------------------      
```                                           

- new 연산자에 의해서 생성되는 객체와 배열은 모두 여기에 생성됨   

## 5. JVM 메모리 구조

* 호출 스택
* 힙
* 메서드 영역(Method Area) = 클래스 영역 = static 영역

```
    - 클래스 정보와 클래스 변수가 저장되는 곳
    - static이 붙은 변수나 메서드가 저장됨.
```

## 6. 메서드 오버로딩 (method overloading) -- new (메서드를 새롭게 추가) 

### 1) 하나의 클래스에 같은 이름의 메서드를 여러개 정의하는 것

```
    - 매개변수 개수나 자료형은 다르지만 메서드명은 같은 메서드를 여러 개 정의하는 것.
```

### 2) 조건

- 메서드 이름이 같아야 함

- 매개변수의 개수 또는 타입, 순서가 달라야 함.

### 3) 성립되지 않는 조건
- 리턴타입이 다른 경우 아무런 영향을 주지 않음

- 매개변수의 이름이 다른 ~~~~

### 4) 장점

- 변수처럼 메서드 이름도 구분이 된다면, 여러개의 이름을 가진 메서드를 구현해야 함.
- 사용자는 그 많은 메서드를 외워야 하고, 개발자들은 메서드 작명하기에 어려움
- 외우기도 싶고 기능도 쉽게 이해할 수 있음    
- 동일하거나 유사한 일을 수행하는 메서드가 전달 받는 매개변수에 따라 각기 다른 연산을 하는 경우 유용함.

```java
class A{
	int data =10;
	int data2 =20;
}
public class Accumulator {
	
	public int add(int x,int y) {
		System.out.println("add(int x,int y)");
		return x + y;
	}
	public long add(int x, long y) {
		System.out.println("add(int x,long y)");
		return x + y;
	}
	
	public long add(long x, int y) {
		System.out.println("add(long x,int y)");
		return x + y;
	}
	
	public double add(double x,double y) {
		System.out.println("add(double x,double y)");
		return x + y;
	}
	//참조형 변수를 받아 오버로딩 하는 케이스
	public int add(A a) {
		System.out.println("add(A a)");
		return a.data + a.data2;
	}
	
}	
```

### 5) vs 오버라이딩 (overriding) -- change , modify