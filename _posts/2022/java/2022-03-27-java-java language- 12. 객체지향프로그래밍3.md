---
title: Java 10. 객체지향프로그래밍 3
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
last_modified_at: '2022-03-27 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

객체지향프로그래밍
===================

## 1.생성자 (constructor)

### 1) 개요
- class_name(argument) {}

```
    - 생성자는 반환값이 없고, 클래스 이름과 동일함
    - 근본적으로 메서드와 같음.
```

- 객체를 생성할 때 new 키워드와 함께 사용 ( 예 : new Student() )
- 객체를 생성하기 위해서 new와 함께 호출 됨.

#### 역할 
- 객체가 생성될 때 변수나 상수를 초기화 하거나 다른 초기화 기능을 수행하는 메서드를 호출함
- 인스턴스가 생성될 때마다, 호출되는 '인스턴스 초기화 메서드' 역할을 함.       
- 대부분의 생성자는 외부에서 접근 가능하지만, 필요에 의해 private으로 선언하는 경우도 잇음.

### 2) 기본 생성자 (default constructor)

- 클래스에는 반드시 적어도 하나 이상의 생성자가 존재
- 클래스에 생성자를 구현하지 않아도 new 키워드와 함께 생성자를 호출할 수 있음.
- 클래스에 생성자가 하나도 없는 경우 컴파일러 생성자 코드를 넣어 줌.

```java
        - public Student(){} 
```

- 매개 변수가 없음, 구현부가 없음

```java
public class Car {

	String color;				// 색상
	String gearType;			// 변속기
	int door;					// 차문
	
	public Car() {
		this.color = "노랑";
		this.gearType = "수동";
		this.door = 4;
	}
	
	// 인스턴스 복제를 위한 생성자
	public Car(Car car) {
		this.color= car.color;
		this.gearType=car.gearType;
		this.door=car.door;
	}
}   
```
### 3) 생성자 만들기    (매개변수가 있는 생성자)

- 컴파일러가 제공해 주는 기본 생성자외에 필요에 의해 생성자를 직접 구현할 수 있다.
- 하나의 클래스에 여러 개의 생성자 사용할 수 있음(오버로딩 개념)
- 클래스에 생성자를 따로 구현하면 기본 생성자(default constructor)는 제공되지 않음.
- 생성자를 호출하는 코드에서 여러 생성자 중 필요에 따라 호출해서 사용할 수 있음.

## 2.this()

* 생성자에서 다른 생성자 호출
* 같은 클래스내에서 다른 생성자를 호출할 때 사용함.
* 다른 생성자 호출은 생성장의 첫문자에서 사용해야 함.
* this와 개념이 다름.

```
- 인스턴스 자신을 가르키는 참조변수
- 인스턴스의 주소가 저장되어 있다.
- 모든 클래스에 지역변수로 숨겨진 채로 존재함.
- new라는 연산자가 heap에 인스턴스를 할당할 때, 비로소 활성화가 이루어짐.
```

```java
public class Car2 {

	String color;				// 색상
	String gearType;			// 변속기
	int door;					// 차문
	
	public Car2() {
		// 같은 클래스내에 있는 매개변수가 3개인 생성자를 호출
		this("검정", "수동", 5);
	}
	public Car2(String color,String gearType,int door) {
		this.color=color;
		this.door=door;
		this.gearType=gearType;
	}
	public Car2(Car2 car) {
		this.color=car.color;
		this.gearType=car.gearType;
		this.door=car.door;
	}
	@Override
	public String toString() {
		return this.color +", "
				+ this.gearType+", "
				+ this.door;
	}
	
	
}
```

## 3.변수의 자료형

### 기본 자료형

```java
    - int, long, float, double 등
```

###  참조 자료형

- String, Studnet, Date 등
- 클래스 형으로 변수를 선언
- 기본 자료형은 사용하는 메모리 크기가 정해져 있지만, 참조 자료형은 클래스에 따라 다름.

## 4.참조 자료형 정의하여 사용하기 (예)

```
1) 학생이 수강한 과목들에 대한 성적을 산출한다.
   ----          ----
   Student      Subject
```

```
   Student                      Subject
    - 학번                     - 과목 이름
    - 이름과                   - 과목 점수
    - 국어과목
    - 수학과목
```

* student

```java
public class Student {
	
	int StudnetID;
	String studentName;
	
	Subject korea;
	Subject math;
	
	public Student(int id, String name) {			//생성자
		this.StudnetID=id;
		this.studentName=name;
		
		korea = new Subject();
		math = new Subject();
	
		
	}
	public void setKoreaSubject(String name,int score) {
		korea.subjectName = name;
		korea.score=score;
	}
	public void setMathSubject(String name,int score) {
		math.subjectName = name;
		math.score=score;
	}
	public void showStudentScore() {
		int total=korea.score+math.score;
		System.out.println(studentName+" 학생의 총점은"+ total +" 입니다.");
	}
	
}
```

* subject

```java
public class Subject {
	
	String subjectName;
	int score;
	int subjectID;
}
```

* Test

```java
public class StudentTest {

	public static void main(String[] args) {

		Student studentLee =new Student(2022, "이순신");
		studentLee.setKoreaSubject("국어", 100);
		studentLee.setMathSubject("수학", 90);
		
		Student studentShin = new Student(2021, "신사임당");
		studentShin.setKoreaSubject("국어", 99);
		studentShin.setMathSubject("수학", 98);
		
		studentLee.showStudentScore();
		studentShin.showStudentScore();
	}

}
```