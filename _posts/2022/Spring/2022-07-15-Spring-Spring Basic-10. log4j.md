---
title: (Spring) 10. log4j를 알아보자!
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: log4j를 알아보자!
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# log4j를 알아보자!

## 1. log4j

---

- 로그 기능을 제공하는 오픈 소스 라이브러리
- 어플리케이션에서 웹 사이트에 접속한 사용자 정보나 각 클래스의 메서드 호출 시각 등  
  여러가지 정보를 로그로 출력해서 관리
- 메이븐에선 프로젝트 생성시 자동으로 **log4j** 라이브러리가 설치됨.

## 2. log4j.xml을 이루는 태그

---

- ex) log4j

```xml
<!-- Appenders -->
	<appender name="console" class="org.apache.log4j.ConsoleAppender">
		<param name="Target" value="System.out" />
		<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%-5p: %c - %m%n" />
		</layout>
	</appender>

    <!-- Application Loggers -->
	<logger name="kr.co.bob">
		<level value="info" />
	</logger>

	<!-- 3rdparty Loggers -->
	<logger name="org.springframework.core">
		<level value="info" />
	</logger>

    ...
```

### 1) `<appender>`

- 로그를 어디에 출력 할것인지 출력 위치를 결정 (콘솔, 파일, db)함
- XXXAppender로 끝나는 클래스들의 이름을 보면 출력 위치를 알수 있음

### 2) `<layout>`

- 어떤 형식으로 출력할지 출력 레이아웃을 결정함

### 3) `<logger>`

- 로깅 메세지를 Appender에 전달함
- 개발자가 로그 레벨을 이용해 로그 출력 여부를 조정 할수 있다.

## 3. Appender 클래스

---

### 1) ConsoleAppender

- 콘솔에 로그 메세지를 출력함

### 2) FileAppender

- 파일에 로그 메세지를 출력함

### 3) RollingFileAppender

- 파일 크기가 일정 기준을 넘으면 기존 파일을 백업 파일로 바꾸고  
  처음부터 다시 기록함.

### 4) DailyRollingFileAppender

- 설정한 기간 단위로 새파일을 만들어 로그 메세지를 기록함.

## 4. PatternLayout 클래스에서 사용하는 출력 속성

### 1) `%p`

- fatal, error, warn, info, debug, trace 등 로그 레벨 이름 출력

### 2) `%m`

- 로그 메세지 출력

### 3) `%d`

- 로깅 이벤트 발생 시각 출력

### 4) `%F`

- 로깅이 발생한 프로그램 파일 이름 출력

### 5) `%M`

- 로깅이 발생한 method 이름 출력

### 6) `%L`

- 로깅이 발생한 caller의 라인 수 출력

...

## 4. DailyRollingFileAppender 추가

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE log4j:configuration PUBLIC "-//APACHE//DTD LOG4J 1.2//EN" "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">

	<!-- Appenders -->
	<!-- ConsoleAppender를 이용해서 로그 메세지를 콘솔로 출력함 -->
	<appender name="console" class="org.apache.log4j.ConsoleAppender">
		<param name="Target" value="System.out" />
		<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%-5p: %c - %m%n" />
		</layout>
	</appender>

	<!-- DailyRollingFileAppender : 로그 메세지를 일별 파일로 출력함-->
	<!-- DailyRollingFileAppender를 이용해서 로그 메세지를 파일로 출력함 -->
	<appender name="dailyFileAppender" class="org.apache.log4j.DailyRollingFileAppender" >
		<param name="File" value="/Users/jeong-won-yeong/Documents/Spring/workspace-spring/logs/output.log" />
		<param name="Append" value="true"/>
		<layout class="org.apache.log4j.PatternLayout">		<!--PatternLayout 출력 형식을 지정 -->
			<param name="DatePattern" value="'.'yyyy-MM-dd" />
			<param name="ConversionPattern" value="[%d{HH:mm:ss}][%-5p](%F:%L)-%m%n" />
		</layout>
	</appender>

	<!-- Application Loggers : 아래 패키지에 존재하는 클래스들의 로그 레벨 설정 -->
	<logger name="kr.co.tiles">
		<level value="debug" />
	</logger>

	<!-- 3rdparty Loggers -->
	<logger name="org.springframework.core">
		<level value="info" />
	</logger>

	<logger name="org.springframework.beans">
		<level value="info" />
	</logger>

	<logger name="org.springframework.context">
		<level value="info" />
	</logger>

	<logger name="org.springframework.web">
		<level value="info" />
	</logger>

	<!-- Root Logger -->
	<root>
		<priority value="warn" />
		<appender-ref ref="console" /> 			<!-- 애플리케이션 전체로그를 콘솔로 출력함 -->
		<appender-ref ref="dailyFileAppender"	<!--  애플리케이션 전체로그를 파일로 출력함 -->
	</root>

</log4j:configuration>

```
