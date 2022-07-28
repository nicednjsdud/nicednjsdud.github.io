---
title: (Spring) 6. MyBatis 란?
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: MyBatis란?
tag: MyBatis
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-05 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# MyBatis

## 1. Intro

### 1) 기존의 JDBC의 이슈

```js
 connecton => statement 객체 생성 => SQL문 전송 => ResultSet 객체반환 => close
```

- sql문이 프로그래밍 코드에 섞여 코드를 복잡하게하여 사용 및 유지보수가 어려워짐.

### 2) Mybatis framework를 도입해서 SQL문 가독성 높여 사용 편리성 만듦

- 코드와 SQL문 분리해서 사용 및 유지보수 편리하게 함.

## 2. 개요

### 1) SQL을 별도 파일(XML)로 분리 관리

- 객체-SQL 사이의 파라미터 Mapping 작업을 자동으로 해줌.

### 2) JDBC 코드 작성의 불편함 제거

- 객체나 DTO 객체 중심으로 개발 가능함

## 3. MyBatis 특징

- 퍼시턴스(Persistence) 프레임 워크
- JDBC의 모든 기능을 대부분 제공
- SQL에 변경이 있을때마다 자바 코드를 수정하거나 컴파일하지 않아도 됨
- 데이터소스(DataSource) 기능과 트랜잭션 처리 기능을 제공

## 4. MyBatis3 주요 컴포넌트

![alt](/assets/images/post/spring/20.png)

### 1) Config.xml (MyBatis 설정 파일)

- 데이터베이스 접속 주소 정보나 Mapping 파일 경로등 고정된 환경정보 설정

### 2) mapping 파일 (mapper.xml)

- sql문과 Mapping 설정

### 3) SqlSessionFactoryBuilder

- SqlSessionFactory를 생성

### 4) SqlSessionFactory

- SqlSession 생성

### 5) SqlSession

- **핵심적인역할**하는 클래스로서 SQL 실행이나 트랜잭션 관리
- Thread-Safe 하지 않으므로 thread마다 필요에 따라 생성함.

## 5. MyBatis-Spring 주요 컴포넌트

![alt](/assets/images/post/spring/21.png)

### 1) SqlSessionFactoryBean

- 설정파일(Config.xml)을 바탕으로 SqlSessionFactory를 생성

### 2) SqlSessionTemplate

- 핵심적인 역할하는 클래스로서 SQL 실행이나 트랜잭션 관리
- Thread-Safe 함
- SqlSession 인터페이스를 구현함.

## 5.5 Test

### 1) pom.xml dependency 추가

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis</artifactId>
			<version>3.5.10</version>
		</dependency>
<!-- https://mvnrepository.com/artifact/
                    com.oracle.database.jdbc/ojdbc8 -->
		<dependency>
			<groupId>com.oracle.database.jdbc</groupId>
			<artifactId>ojdbc8</artifactId>
			<version>21.6.0.0.1</version>
		</dependency>
```

### 2) MemberDTO 생성

- MemberDTO.java

```java
package kr.co.mybatis.orm01;

import java.sql.Date;

public class MemberDTO {

	private String id;
	private String pwd;
	private String name;
	private String email;
	private Date joinDate;

	// 생성자

	public MemberDTO() {
	}

	public MemberDTO(String id, String pwd, String name, String email) {
		this.id = id;
		this.pwd = pwd;
		this.name = name;
		this.email = email;
	}
    // 게터/세터 생성
    ...
```

### 3) mapper.xml 생성

- member.xml

<a><b>Mybatis에서 <![CDATA]>를 사용하는 이유<b><a>

## 6. SqlSession 클래스에서 제공하는 메소드

### 1) List selectList(id)

- id에 대한 select문 실행한 후 여러 레코드들 List로 반환함

### 2) T selectOne(id)

- id에 대한 select문 실행한 후 한 개의 레코드 반환함

### 3) int insert(id)

- id에 대한 insert문 실행하면서 obj 객체의 값을 테이블에 추가함

### 4) int Update(id,Object obj)

- obj 객체의 값을 조건문의 수정 값으로 사용해 id에 대한 update문 실행

### 5) int delete(id,Object obj)

- obj 객체의 값을 조건문의 조건 값으로 사용해 id에 대한 delete문 실행

## 7. 마이바티스로 조건 값 전달 방법

### 1) SQL문에서 조건 값 사용방법

```
	#{전달된 매개변수 이름}
```

## 8. 마이바티스 동적 SQL문

### 1) 주로 SQL문의 조건절에서 사용

- 조건절 (where)에 조건을 동적으로 추가

### 2) JSTL과 XML기반으로 동적 SQL문 작성

- if
- choose(when, otherwise)
- trim()
- foreach

### 3) `<if>`태그

```xml
	<where>
		<if test='조건식'>
			추가할 구문
		</if>
	</where>
```

- ex)

```xml
	<select id = "searchMember" parameterType="memberDTO" resultMap="memResult">
		<!-- 공통 SQL문  -->
		<![CDATA[
			SELECT * from T_MEMBER
		]]>
		<where>
			<if test="name !='' and name !=null">
				name = #{name}
			</if>
			<if test="email !='' and email !=null">
				and email = #{email}
			</if>
		</where>
			order by joinDate desc

	</select>

```

### 4) `<choose>`태그

```xml
	<choose>
		<when test="조건식1">
			구문1
		</when>
		<when test="조건식2">
			구문2
		</when>
		...
		<otherwise>
			구문 n + 1
		</otherwise>
	</choose>
```
