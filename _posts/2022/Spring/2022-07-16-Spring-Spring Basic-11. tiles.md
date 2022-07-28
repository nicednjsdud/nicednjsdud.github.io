---
title: (Spring) 11. Tiles Framework
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Tiles Framework
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Tiles

## 1. 타일즈(tiles)

---

- 화면의 레이아웃 기능을 제공하는 오픈 소스 라이브러리
- 페이지 레이아웃을 쉽고 단순하게 구현할 수 있음
- 공통된 레이아웃을 사용하므로 유지관리가 용이함.

* 반복적으로 사용되는 부분들에 대한 코드를 분리해서 예브게 한곳에 관리 ex) **header,sidebar,footer**

## 2. JSP include와의 차이

---

- jsp는 페이지 내에 동일한 레이아웃 정보가 들어가므로 전체적인 레이아웃을 변경하게될 경우
  - 모든 페이지를 수정해야 하는 단점
- tiles는 이런 일이 있으면 설정 파일만 변경해주면 된다.

### 1) tiles 라이브러리 추가

```xml
	<!-- 타일즈 관련 라이브러리 -->
		<!-- https://mvnrepository.com/artifact/org.apache.tiles/tiles-core -->
		<dependency>
			<groupId>org.apache.tiles</groupId>
			<artifactId>tiles-core</artifactId>
			<version>2.2.2</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.apache.tiles/tiles-jsp -->
		<dependency>
			<groupId>org.apache.tiles</groupId>
			<artifactId>tiles-jsp</artifactId>
			<version>2.2.2</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.apache.tiles/tiles-servlet -->
		<dependency>
			<groupId>org.apache.tiles</groupId>
			<artifactId>tiles-servlet</artifactId>
			<version>2.2.2</version>
		</dependency>
```

### 2) servlet-content.xml 변경

- tiles의 맞춰 변경한다.

```xml
	<!-- tiles viewResolver를 사용해 화면 표 -->
	<beans:bean id="viewResolver"
		class="org.springframework.web.servlet.view.UrlBasedViewResolver">
		<beans:property name="viewClass"
			value="org.springframework.web.servlet.view.tiles2.TilesView" />
	</beans:bean>

	<!--tiles 관련 빈 설정 - TilesConfigurer 클래스를 이용해 빈 생성 -->
	<beans:bean id="TilesConfigurer"
		class="org.springframework.web.servlet.view.tiles3.TilesConfigurer">
		<beans:property name="definitions">
			<beans:list>
				<!-- tiles의 모든 설정 XML 파일을 읽어들 -->
				<beans:value>classpath:tiles/*.xml</beans:value>
			</beans:list>
		</beans:property>
		<beans:property name="PreparerFactoryClass"
			value="org.springframework.web.servlet.view.tiles3.SpringBeanPreparerFactory" />
	</beans:bean>
	<context:component-scan
		base-package="kr.co.tiles" />

```

### 3) src/main/resources tiles_member.xml 추가

- tiles 패키지를 만든뒤 그 안에 tiles_member.xml 파일을 넣어줌

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE tiles-definitions PUBLIC
       "-//Apache Software Foundation//DTD Tiles Configuration 2.1//EN"
       "http://tiles.apache.org/dtds/tiles-config_2_1.dtd">
<tiles-definitions>
	<!-- baseLayout : 공통 레이아웃의 뷰 이름을 지정 template : 전체 레이아웃을 정하는 JSP 위치 지정 -->
	<definition name="baseLayout"
		template="/WEB-INF/views/common/layout.jsp">
		<!-- 레이아웃 상단(헤더)을 구성하는 jsp -->
		<put-attribute name="title" value="" />	<!-- 변동할수 있게 값을 비워둠 -->
		<put-attribute name="header"
			value="/WEB-INF/views/common/header.jsp" />
		<!-- 레이아웃 사이드 메뉴를 구성하는 jsp -->
		<put-attribute name="side"
			value="/WEB-INF/views/common/side.jsp" />
		<put-attribute name="body" value="" />
		<put-attribute name="footer"
			value="/WEB-INF/views/common/footer.jsp" />
	</definition>

	<!-- 메인 화면의 뷰이름 -->			<!-- 기본 레이아웃은 baseLayout을 상속받음 -->
	<definition name="main" extends="baseLayout">
		<put-attribute name="title" value="메인페이지" />
		<put-attribute name="body"
			value="/WEB-INF/views/main.jsp" />
	</definition>

	<!-- 컨트롤러에서 반환되는 뷰이름 지정 --> <!-- 기본 레이아웃을 상속받음 -->
	<definition name="/member/listMembers" extends="baseLayout">
		<put-attribute name="title" value="회원목록" />
		<put-attribute name="body"
			value="/WEB-INF/views/member/listMembers.jsp" /><!-- 레이아웃 페이지의 본문에 표시할
			JSP지정 -->
	</definition>

	<definition name="/member/loginForm" extends="baseLayout">
		<put-attribute name="title" value="로그인창" />
		<put-attribute name="body"
			value="/WEB-INF/views/member/loginForm.jsp" />
	</definition>
</tiles-definitions>
```

![alt](/assets/images/post/spring/30.png)
