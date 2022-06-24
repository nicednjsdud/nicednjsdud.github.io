---
title: JSP 16. JSTL 국제화 태그
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JSP and Servlet
description: JSP
tag : JSTL
article_tag1: JSP
article_section: JSP
meta_keywords: java,java JSP, JDBC
last_modified_at: '2022-06-13 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JSTL 국제화 태그
=================

## 1. 국제화(Formatting) 태그

* 국가별 다양한 언어, 날짜, 시간, 숫자 형식을 설정할 때 사용됨
* 태그 종류
    * 숫자 포맷, 날자 포맷, 타임존 설정, 로케일 설정

### 1) 숫자 포맷

```html
<fmt:formatNumber value="출력할 숫자" 
                  type="출력 양식(percent,currency,number)" 
                  var="출력할 숫자를 변수에 저장" 
                  groupingUsed="세자리마다 콤마 출력 여부, 기본값은 true" 
                  pattern="출력할 숫자 양식"  />
```

* fmt.jsp

```html

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSTL - fmt</title>
</head>
<body>
	<h4>숫자 포맷</h4>
	<c:set var="number1" value="12345" /> 
    <!-- 숫자를 값으로 갖는 변수 선언 -->
	<fmt:formatNumber value="${number1 }"  /><br><br>
	<!-- 기본적으로 큰수는 세자리마다 콤마출력 -->

	<fmt:formatNumber value="${number1 }" groupingUsed="false" />
	<br><br>
	<!-- var 속성 사용으로 즉시 출력하지 않고 지정한 위치에 출력함 -->
	<fmt:formatNumber value="${number1 }" type="currency" var="printNumber1"/>
	통화기호 : ${printNumber1 } 
	<br><br>
	<fmt:formatNumber value="0.03" type="percent" var="printNumber2"/>
	퍼센트 : ${printNumber2 }
</body>
```

![alt](/assets/images/post/jsp/134.png)

### 2) 날짜,시간 포맷

```html
	<fmt:formatDate value="출력할 날짜" 
					type="출력 양식" 
					dateStyle="날짜 스타일" 
					timeStyle="시간 스타일" 
					var="변수 설정"
					scope="영역" 
					pattern="날짜 패턴"/>
```

#### 태그 속성

* type : 날짜(date), 시간(time),날짜 및 시간(both)
* dateStyle : default, short, medium, long, full 중 선택
* timeStyle : default, short, medium, long, full 중 선택

```html
<c:set var="today" value="<%= new Date() %>" />
	
<h4>날짜 포맷<h4>
full : <fmt:formatDate value="${today }" type="date" dateStyle="full"/>
<br>
short : <fmt:formatDate value="${today }" type="date" dateStyle="short"/>
<br>
long : <fmt:formatDate value="${today }" type="date" dateStyle="long"/>
<br>
default : <fmt:formatDate value="${today}" type="date" dateStyle="default"/>
<br><br>
	
<h4>시간 포맷</h4>
full : <fmt:formatDate value="${today }" type="time" timeStyle="full"/>
<br>
short : <fmt:formatDate value="${today }" type="time" timeStyle="short"/>
<br>
long : <fmt:formatDate value="${today }" type="time" timeStyle="long"/>
<br>
default : <fmt:formatDate value="${today}" type="time" timeStyle="default"/>
<br>
	
<h4>날짜 시간 포맷</h4>
<fmt:formatDate value="${today }" type="both" dateStyle="full" 
												timeStyle="full"/><br>
<fmt:formatDate value="${today }" type="both" 
						pattern="yyyy-MM-dd hh:mm:ss"/><br>
```

![alt](/assets/images/post/jsp/135.png)

### 3) 타임존

```html
<h4>타임존</h4>
	<fmt:timeZone value="GMT">	<!-- 세계협정시 -->
		<fmt:formatDate value="${today }" type="both" 
						dateStyle="full" timeStyle="full"/>
		<br>
	</fmt:timeZone>
	<fmt:timeZone value="America/Chicago"> <!-- 특정지역명 -->
		<fmt:formatDate value="${today }" type="both" 
						dateStyle="full" timeStyle="full"/>
	</fmt:timeZone>

```

![alt](/assets/images/post/jsp/136.png)

### 4) 로케일

```html
	<h4>로케일</h4>
	<c:set var="today" value="<%= new Date() %>" />
	
	한글로 설정 : <fmt:setLocale value="ko_kr"/>
	<fmt:formatNumber value="10000" type="currency"/><br>
	<fmt:formatDate value="${today }"/><br><br>
	
	영어로 설정 : <fmt:setLocale value="en_US"/>
	<fmt:formatNumber value="10000" type="currency"/><br>
	<fmt:formatDate value="${today }"/><br><br>
	
	프랑스어로 설정 : <fmt:setLocale value="ca_FR"/>
	<fmt:formatNumber value="10000" type="currency"/><br>
	<fmt:formatDate value="${today }"/><br>
```


![alt](/assets/images/post/jsp/137.png)

## 2. XML 태그

* XML 문서를 처리하기 위한 것

### 1) eXtensible Markup Language

* 태그를 개발자가 직접 정의할수 있고 데이터를 기술할 수 있는 언어임.
* 데이터 전달 역할

### 2) xml 태그 종류

#### parse

* XML을 파싱할때 사용

#### out

* select 속성에 저장한 XPath 표현식의 결과를 출력함.

#### forEach

* select 속성에 지정한 xPath 표현식의 값을 다중 조건으로 결정함
* 하위에 when, otherwise 태그 사용함.

#### XPath

* XML 문서의 요소(Element)에 접근하기 위해 사용함.
* XML 문서의 노드를 식별하고 탐색하는 역할

#### bookList.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<booklist>
	<book>
		<name>실무자를 위한 딥러닝</name>
		<author>로널드 크누젤</author>
		<price>40000</price>
		
		<name>A/B 테스트</name>
		<author>론 코하비</author>
		<price>30000</price>
	</book>
</booklist>
```

