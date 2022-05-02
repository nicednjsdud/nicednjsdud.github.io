---
title: Java 21. 인터페이스
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is Interface?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, interface
last_modified_at: '2022-04-04 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

인터페이스
===========

## 인터페이스(interface)

* 일종의 추상클래스이긴 하나 멤버의 주류가 추상메서드임.

```
    - 모든 메서드 추살 메서드로 선언됨 (public abstract)
    - 모든 변수는 상수로 선언됨 (public static final) 
```       
       
* 상속 관계가 아닌 클래스에 기능을 제공하는 구조임.

### 멤버
- 추상메서드, 상수 
- 디폴트 메서드, 정적 메서드, private 메서드 멤버도 추가되어 활용성이 높아짐.

```java    
        interface A {                               interface A {
            public abstract void say();                     void say();
            public static final int a = 2;    ==>           int a =2;
        }                                           }
```

* 생성자가 없음. => 인스터스를 만들수 없음.
* 표준을 제시하며, 그 규칙에 맞게 구현하도록 함.
* 다형성 개념이 적용됨.

## 인터페이스 정의와 구현

### 인터페이스 구현
- extends를 사용하지 않고 implements를 사용함.
- 클래스를 상속하는 것과 동일한 개념.
- 인터페이스도 일종의 조상임(다형성 개념이 적용됨) 
- 구현클래스는 반드시 인터페이스에 선언되어 있는 추상메서드를 재정의해야 한다.

### 형 변환
- 인터페이스를 구현한 클래스는 인터페이스 형으로 선언한 변수로 형 변환됨.

```java
            Calc calc = new ComleteCalc();
```

- 상속에서의 형변환과 동일한 의미
- 형반환되는 경우 인터페이스에 선언된 메서드만 사용 가능함.

## 인터페이스가 하는 역할

* 클래스나 프로그램이 제공하는 기능을 명시적으로 선언
* 일종의 클라이언트 코드와의 약속이며 클래스나 프로그램이 제공하는 명세(specification)
* 클라이언트 프로그램은 인터페이스에 선언된 메서드 명세만 보고 이를 구현한 클래스를 사용할 수 있다.

* 인터페이스를 구현한 다양한 객체를 사용함 - 다형성
* 예) JDBC 인터페이스 

## 인터페이스를 활용성 다형성 구현

### DAO : database access object 구현하기

* 하나의 인터페이스를 여러 객체가 구현하게 되면 클라이언트 프로그램은 인터페이스의  
  메서드를 활용하여 여러 객체의 구현을 사용할수 있음. ( 다형성 )

###  인터페이스를 활용한 dao 구현하기
- DB에 회원 정보를 넣는 dao를 여러 DB 제품에 지원될수 있게 구현함.
- 환경파일(db.properties)에서 database의 종류에 대한 정보를 읽고  
  그 정보에 맞게 dao 인스턴스를 생성하여 실행될수 있게 함.
  
```java
public class UserInfo {
	
	private String userId;
	private String passWd;
	private String userName;
	
	public String getUserId() {
		return userId;
	}
	public void setUserId(String userId) {
		this.userId = userId;
	}
	public String getPassWd() {
		return passWd;
	}
	public void setPassWd(String passWd) {
		this.passWd = passWd;
	}
	public String getUserName() {
		return userName;
	}
	public void setUserName(String userName) {
		this.userName = userName;
	}
	
	
}
```

```java
import kr.co.ezenac.domain.userinfo.UserInfo;

public interface UserInfoDao {
	
	void insertUserInfo(UserInfo userInfo);
	void updateUserInfo(UserInfo userInfo);
	void deleteUserInfo(UserInfo userInfo);
	
}
```

```java
import kr.co.ezenac.domain.userinfo.UserInfo;
import kr.co.ezenac.domain.userinfo.dao.UserInfoDao;

public class UserInfoMsSqlDao implements UserInfoDao {

	@Override
	public void insertUserInfo(UserInfo userInfo) {
		System.out.println("insert into MsSql DB userId = "+userInfo.getUserId());

	}

	@Override
	public void updateUserInfo(UserInfo userInfo) {
		System.out.println("update into MsSql DB userId = "+userInfo.getUserId());

	}

	@Override
	public void deleteUserInfo(UserInfo userInfo) {
		System.out.println("delete into MsSql DB userId = "+userInfo.getUserId());

	}

}
```


```
    db.properties

    DBTYPE=MSSQL
```

## 인터페이스의 멤버

### 상수
- 모든 변수는 상수로 변환됨.
- public static final

### 추상메서드
- 모든 선언된 메서드는 추상 메서드
- public abstract

### default 메서드 (java 8이후)
- 구현을 가지는 메서드
- 공통으로 사용할 수 있는 기본 메서드
- default 키워드 사용
- 구현하는 클래스에서 재정의 할수도 있음.

### 정적 메서드 (java 8 이후)
- 인스턴스 생성과 상관없이 인터페이스 타입으로 사용할 수 있는 메서드

### private 메서드 (java 9 이후)
- 인터페이스를 구현한 클래스에서 사용하거나 재정의 할 수 없음.
- 인터페이스 내부에서만 사용하기 위해 구현하는 메서드
- default 메서드, 정적 메서드에서 사용함.

## 여러 인터페이스 구현, 인터페이스의 상속

* 자바의 인터페이스는 구현 코드가 없으므로 하나의 클래스가 여러 인터페이스는 구현 할 수 있음.
* 디폴트 메서드가 중복되는 경우 구현하는 클래스에서 재정의하여야 함.
* 여러 인터페이스를 구현한 클래스는 인터페이스 타입으로 형변환되는 경우  
   해당 인터페이스에 선언된 메서드만 사용 가능함.
### 인터페이스의 상속
- 인터페이스 사이에도 상속을 사용할 수 있음.
- extends 키워드를 사용
- 인터페이스는 다중 상속이 가능함.
- 인터페이스는 다중 상속이 가능함. (타입 상속)
* 클래스 상속과 인터페이스 구현 함께 쓰기

* Calc

```java

public interface Calc {
	
	double PI = 3.14;
	int ERROR = -99999999;
	
	int add(int num1,int num2);
	int substract(int num1,int num2);
	int times(int num1,int num2);
	int divide(int num1,int num2);
	
}
```

* Calculator

```java
package kr.co.ezenac.interface2;

public abstract class Calculator implements Calc {

	@Override
	public int add(int num1, int num2) {
		
		return num1+num2;
	}
	@Override
	public int substract(int num1, int num2) {
		
		return num1-num2;
	}
}
```

* CompletCalc

```java
public class CompletCalc extends Calculator {
	
	@Override
	public int times(int num1, int num2) {
		return num1*num2;
	}
	@Override
	public int divide(int num1, int num2) {
		if(num2 ==0) {	
			return ERROR;
		}
		else {
			return num1 /num2;
		}
	}
}
```

* Test

```java
public class CalculatorTest {

	public static void main(String[] args) {

		Calc calc =new CompletCalc();
		int num1 =10;
		int num2 = 2;
		
		System.out.println(num1 +"+"+ num2 +"="+calc.add(num1, num2));
		System.out.println(num1 +"-"+ num2 +"="+calc.substract(num1, num2));
		System.out.println(num1 +"*"+ num2 +"="+calc.times(num1, num2));
		System.out.println(num1 +"/"+ num2 +"="+calc.divide(num1, num2));
			
	}

}
```