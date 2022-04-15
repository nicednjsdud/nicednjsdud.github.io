---
title: Java 13. 객체지향프로그래밍 4
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
last_modified_at: '2022-03-28 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

객체지향프로그래밍
===================

## 1.캡슐화 (encapuslation)

### 정보 은닉을 활용한 캡슐화

* 꼭 필요한 정보와 기능만 외부에 오픈함
* 대부분의 멤버 변수와 메서드를 감추고 외보에서 통합된   
  인터페이스만은 제공하여 일관된 기능을 구현하게 함.
* 각각의 메소드나 멤버변수를 접근함으로써 발생하는 오류를 최소화 함.

```java
	private int busNumber;
	private int passengerCount;
	private int money;
```

## 2.객체간의 협력 (collabration)

* 객체지향 프로그램에서 객체 간에는 협력이 이루어짐
* 협력을 위해서는 필요한 메세지를 전송하고, 이를 처리하는 기능이 구현되어야 함.

* 매개 변수로 객체가 전달되는 경우가 발생.
* 객체의 협력 

```
    ex) 버스를 탄다.
        지하철을 탄다.
                                    버스
    학생                            - 버스번호
     - 이름                          - 승객 수
     - 학년      ---------------->   - 수입      
     - 가진돈                        - 타다
                                     지하철        
        |                           - 노선번호           
        |------------------------>  - 승객 수
                                    - 수입 
                                    - 타다 
```

* lab

```
        - 이순신은 지각을 해서 택시를 타야 했습니다.
          이순신은 20000원을 가지고 있었는데, 10000원을 택시비로 사용함
          택시는 'BoB 운수' 회사 택시를 탔습니다.

        - 출력 결과 ->
            - 이순신님의 남은 돈은 10000원입니다.
              BoB 운수택시 수입은 10000원입니다.  
```

* person

```java
public class Person {
	private String personName;
	private int money;
	
	public Person(String personName,int money) {
		this.personName=personName;
		this.money=money;
	}
	
	public void takeTaxi(Taxi taxi) {
		taxi.take(10000);
		this.money -=10000;
	}
	public void PersonInfo() {
		System.out.println(personName+"님의 남은 돈은"+money+"입니다.");
	}
}
```

* Taxi

```java
public class Taxi {
	private String taxiName;
	private int money;
	
	public Taxi(String taxiname) {
		this.taxiName=taxiname;
	}
	public void take(int money) {
		this.money +=money;
	}
	public void taxiInfo() {
		System.out.println(taxiName+" 운수택시 수입은"+money+"입니다.");
	}	
}
```

* Test

```java
public class PersonTest {

	public static void main(String[] args) {
		Person person= new Person("이순신",20000);
		Taxi taxi= new Taxi("BoB");
		
		person.takeTaxi(taxi);
		person.PersonInfo();
		taxi.taxiInfo();
	}

}
```
