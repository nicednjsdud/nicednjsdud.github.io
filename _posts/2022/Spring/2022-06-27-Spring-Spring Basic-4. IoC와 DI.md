---
title: (Spring) 3. Ioc 와 DI 컨테이너
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Spring Framework description
tag: Spring Basic
article_tag1: Spring Basic
article_section: Spring Basic
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-06-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# IoC와 DI 컨테이너

## 0. 컨테이너(Container) 란?

- 컨테이너는 인스턴스의 생명주기를 관리한다.
- 생성된 인스턴스들에게 추가적인 기능을 제공한다.

## 1. IoC (Inversion of Control)

![alt](/assets/images/post/spring/3.png)

1. '도치,역전'이다. 객체의 생성, 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀌였음.
2. 객체의 생성을 책임지고,의존성 관리함
3. POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가짐
4. 개발자들이 직접 POJO를 생성할수 있지만 컨테이너에게 맡김

## 2. IoC의 분류

### 1) DL (Dependency Lookup)

#### 의존성 검색

### 2) DI (Dependency Injection)

#### 의존성 주입

- 각 클래스간의 의존관계를 빈 설정 (Bean Definition)정보를 바탕으로  
  컨테이너가 자동으로 연결해주는 것

- Setter Injection
- Constructor Injection
- Method Injection

## 3. DI

1. 개발자들은 단지 빈 설정파일에서 의존관계가 필요하다는 정보를 추가하면 됨.
2. 객체 레퍼런스를 컨테이너로부터 주입 받아서, 실행 시에 동적으로 의존관계가  
   생성됨.
3. 컨테이너가 흐름의 주체가 되어 애플리케이션 코드에 의존관계를 주입해 주는 것

### 4. 장점

- 코드가 단순해짐
- 컴포넌트 간 결합도가 제거됨

## 4. DI 유형

### 1) Setter Injection

- Setter 메서드를 이용한 의존성 삽입

### 2) Constructor Injection

- 생성자를 이용한 의존성 삽입

### 3) Method Injection

- 일반 메서드를 이용한 의존성 삽입

## 5. Spring DI 컨테이너

- Spring DI 컨테이너가 관리하는 객체를 빈(bean)이라고 하고, 이 빈(bean)들을  
  관리한다는 의미로 컨테이너를 **빈팩토리(BeanFactory)**라고 부름.
- 객체의 생성과 객체 사이의 런타임 관계를 DI 관점에서 볼때는 컨테이너를  
  **BeanFactory** 라고 함.
- BeanFactory에 여러가지 컨테이너 기능을 추가하여 **애플리케이션 컨텍스(ApplicationContext)**  
  라고 부름

### 1) BeanFactory

- Ioc/DI에 대한 기본 기능을 가지고 있다.
- Bean을 등록, 생성, 조회, 반환 관리함.
- getBean() 메서드가 정의되어 있음

### 2) ApplicationContext

- Bean을 등록, 생성, 조회, 반환 관리함.
- Spring의 각종 부가 서비스를 추가로 제공함.
- Spring이 제공하는 ApplicationContext 구현 클래스가 여러가지 종류가 있음.
- 트랜잭션 처리, AOP등에 대한 처리를 할 수있다.

## 6. Spring DI 용어

### 1) 빈(Bean)

- 스프링이 IoC 방식으로 관리하는 객체라는 뜻
- 스프링이 직접 생성과 제어를 담당하는 객체를 Bean이라고 부름

### 2) 빈팩토리 (BeanFacotory)

- 스프링이 IoC 담당하는 핵심 컨테이너를 가리킴.
- Bean을 등록, 생성, 조회, 반환하는 기능을 담당함.

### 3) 애플리케이션 컨텍스트(ApplicationContext)

- BeanFactory를 확장한 IoC 컨테이너

### 4) 설정 메타정보(Configuration metadata)

- ApplicationContext 또는 BeanFactory가 IoC를 적용하기 위해 사용하는  
  메타 정보를 말함.

## 7. Bean 의존관계 설정 방법

### 1) Setter Injection

- Setter 메서드를 통해 의존관계가 있는 Bean을 주입하려면 `<property>`태그를 사용
- value 속성은 단순 값 또는 Bean이 아닌 객체 주입
- ref 속성은 Bean 이름 이용

#### 1. PersonService 인터페이스 생성

```java
package kr.co.ezenac.di;
public interface PersonService {public void sayHello();}
```

#### 2. PersonServiceImpl 객체 생성

```java
package kr.co.ezenac.di;

public class PersonServiceImpl implements PersonService {
	private String name;
	private int age;

	public void setName(String name) {this.name = name;}
	@Override
	public void sayHello() {
		System.out.println("이름 : "+name);
		System.out.println("나이 : "+age);
	}
}
```

#### 3. Person.xml 생성

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN 2.0//EN"
        "http://www.springframework.org/dtd/spring-beans-2.0.dtd">
<beans>
	<!-- bean 태그 이용해 PersonServiceImpl 객체(빈)을 생성한 후 빈 id를 personService로 지정 -->
	<bean id="personService" class="kr.co.ezenac.di.PersonServiceImpl">
	<!-- PersonServiceImpl 객체의 속성 name값을 value태그를 이용해 초기화 -->
		<property name="name">
			<value>정원영</value>
		</property>
	</bean>
</beans>
```

#### 4. Test

```java
package kr.co.ezenac.di;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.FileSystemResource;

public class PersonTest {

	public static void main(String[] args) {
		// 실행시 person.xml을 읽어 들여 빈을 생성
		BeanFactory factory = new XmlBeanFactory(new FileSystemResource("person.xml"));
		// id가 personService인 빈 가져옴
		PersonService ac = (PersonService) factory.getBean("personService");
		// 자바 코드에서 객체 직접 생성하지 않아도 됨.
		//PersonService personService = new PersonServiceImpl();
		// 생성된 빈을 이용해 name값 출력
		ac.sayHello();
	}
}
```

![alt](/assets/images/post/spring/4.png)

### 2) Constructor Injection

- Constructor를 통해 의존관계가 있는 Bean을 주입하려면 `<constructor-arg>`  
  태그를 사용

#### 1. PersonService 인터페이스 생성

- 위와 동일

#### 2. PersonService 객체 생성

- 위 코드에서 생성자만 추가

```java
// person.xml에서 인자가 한개인 생성자 설정시 사용
	public PersonServiceImpl(String name) {this.name = name;}

// person.xml에서 인자가 두개인 생성자 설정시 사용
	public PersonServiceImpl(String name, int age) {
		this.name = name;
		this.age = age;
	}
```

#### 3. Person.xml 추가

- 위 코드에서 빈 2개 추가

```xml
<!-- 인자가 한개인 생성자로 id가 personService1인 빈 생성함
	  생성자로 value인 '정원영'을 전달 => 속성 name을 초기화  -->
	<bean id="personService1" class="kr.co.ezenac.di02.PersonServiceImpl">
		<constructor-arg value="정원영" />
	</bean>

<!-- 인자가 두개인 생성자로 id가 personService2인 빈 생성함
	  생성자로 두개의 값을 전달 => 속성 name,age를 초기화  -->
	<bean id="personService2" class="kr.co.ezenac.di02.PersonServiceImpl">
		<constructor-arg value="BoB" />
		<constructor-arg value="26" />
	</bean>
```

#### 4. Test

```java
package kr.co.ezenac.di02;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.FileSystemResource;

public class PersonTest {

	public static void main(String[] args) {
		// 실행시 person.xml을 읽어 들여 빈을 생성
		BeanFactory factory = new XmlBeanFactory(new FileSystemResource("person.xml"));

		PersonService ac = (PersonService) factory.getBean("personService1");
		PersonService ac1 = (PersonService) factory.getBean("personService2");
		// 자바 코드에서 객체 직접 생성하지 않아도 됨.
		//PersonService personService = new PersonServiceImpl();

		ac.sayHello();
		ac1.sayHello();
	}
}

```

![alt](/assets/images/post/spring/5.png)

### 3) Method Injection

#### 1. SpringDITest 생성

```java
package kr.co.ezenac.di04;

import java.util.Arrays;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;
import org.springframework.stereotype.Component;

class Engine {
}

class Door {
}

class Car {
	String color;
	int oil;

	public Car() {
	}

	Engine engine;
	Door[] doors;

	public Car(String color, int oil, Engine engine, Door[] doors) {
		super();
		this.color = color;
		this.oil = oil;
		this.engine = engine;
		this.doors = doors;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public void setOil(int oil) {
		this.oil = oil;
	}

	public void setEngine(Engine engine) {
		this.engine = engine;
	}

	public void setDoors(Door[] doors) {
		this.doors = doors;
	}
	@Override
	public String toString() {
		return "Car{" + "color : " + this.color + ", oil : " + this.oil + ", engine : " + this.engine + ", door : "
				+ Arrays.toString(doors) + "}";
	}
}
@Component
public class SpringDITest {
	public static void main(String[] args) {
		ApplicationContext ac = new GenericXmlApplicationContext("config.xml");
		Car car = (Car) ac.getBean("car");
		System.out.println("car :"+car);
	}
}
```

#### 2. config.xml 생성

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="car" class="kr.co.ezenac.di04.Car">
		<constructor-arg name="color" value="red" />
		<constructor-arg name="oil" value="100" />
		<constructor-arg name="engine" ref="engine" />
		<constructor-arg name="doors">
			<array value-type="kr.co.ezenac.di04.Door">
				<ref bean="door" />
				<ref bean="door" />
			</array>
		</constructor-arg>

	</bean>

	<bean id="engine" class="kr.co.ezenac.di04.Engine" />
	<bean id="door" class="kr.co.ezenac.di04.Door" scope="singleton" />
</beans>
```

![alt](/assets/images/post/spring/6.png)

## 8. 프로퍼티(Property) 값 설정 방법

### 1) 단순 값 (문자열, 숫자)의 주입(Injection)

### 2) 컬렉션 (Collection) 타입의 값 주입(Injection)

- List, Set, Map, Properties와 같은 타입을 XML로 작성해서  
  프로퍼티에 주입하는 방법

#### List, Set 타입

- `<list>,<set>,<value>` 태그를 이용

## 9. Bean 등록 메타정보 구성 전략

### 1) 전략(1) : XML 단독 사용

- 모든 Bean을 명시적으로 XML에 등록하는 방법
- Bean 개수가 많아지면 관리하기 번거로울수 있음
- 설정파일을 공유해서 개발하다 보면 동시에 수정, 충돌 발생
- 적절한 setter 메서드, constructor가 코드내에 반드시 존재해야 함.

### 2) 전략(2) : XML과 빈 스캐닝(Bean Scanning)의 혼용

- Bean으로 사용될 클래스에 특별한 어노테이션(Annotation)을 부여해주면  
  이런 클래스를 자동으로 찾아서 Bean으로 등록함.

- 특정 어노테이션이 붙은 클래스 자동으로 찾아서 Bean으로 동록해주는 방식을  
  빈 스캐닝(Bean Scanning)을 통한 자동인식 Bean 등록 기능이라고 함.
