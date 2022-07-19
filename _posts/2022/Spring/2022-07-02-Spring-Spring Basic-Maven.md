---
title: (Spring) 4. Maven 이란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Maven
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-02 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Maven

## 1. Maven 이란?

- 프로젝트 구조와 내용을 기술하는 선언적 접근 방식의 오픈 소스 빌드 툴
- 프로젝트 종속 라이브러리들과 그 라이브러리에 의존하는 Dependency 자원까지 관리 가능
  - 편리한 Dependent Library 관리
  - 여러 프로젝트에서 프로젝트 정보나 jar 파일들을 공유하기 쉬움
  - pom.xml 파일 수정
- 프로젝트 전반의 리소스 관리와 설정 파일 그리고 이와 관련된 표준디렉토리 구조를 처음부터  
  일관된 형채로 구성하여 관리 가능
  - 모든 프로젝트의 빌드 프로세스를 일관되게 가져갈 수 있음.

## 2. 메이븐 프로젝트 구성 요소

### 1) pom.xml

- Maven 프로젝트를 생성하면 pom.xml 파일 생성됨
- Project Object Model 정보를 담고 있음
- 외존 관계 (Dependency) 추가 <a href="https://mvnrepository.com/">mvn 검색</a>

### 2) src/main/java

- 자바 소스 파일 위치함

### 3) src/main/resources

- 프로퍼티 파일이나 xml파일 등 리소스 파일이 위치함

### 4) src/test/java

- JUnit 등 테스트 파일 위치

### 5) src/test/resources

- 테스트시 필요한 resources 파일이 위치함

### 6) src/main/webapp

- WEB-INF 등 웹 애플리케이션 리소스가 위치함.

## 3. pom.xml의 구성 요소

### 1) 프로젝트 정보 설정 태그

- ex) pom.xml

```xml
<modelVersion>4.0.0</modelVersion>
	<groupId>kr.co</groupId>
	<artifactId>bob</artifactId>
	<name>ezen08_Spring_Annotation</name>
	<packaging>war</packaging>
	<version>1.0.0-BUILD-SNAPSHOT</version>
```

#### groupId

- 프로젝트 그룹 id를 나타냄
- 일반적으로 도메인 이름을 사용해 설정함

#### artifactId

- 프로젝트 아티팩트 id를 설정함
- 대개 패키지 이름으로 설정함

### 2) dependencies 정보 설정 태그

```xml
<dependency>
	<groupId>org.aspectj</groupId>
	<artifactId>aspectjrt</artifactId>
	<version>${org.aspectj-version}</version>
</dependency>
```

#### dependency

- 해당 프로젝트에서 의존하는 다른 라이브러리 정보 기술

#### groupId

- 의존하는 프로젝트 그룹 id

#### artifactId

- 의존하는 프로젝트 artifactId
