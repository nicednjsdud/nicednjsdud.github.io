---
title: JSP 15. JSTL
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
last_modified_at: '2022-06-10 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JSTL
======

## 1. JSTL이란?

* JSP Standard Tag Libaray
* 조건문,반복문 등을 처리해주는 태그를 모아 표준으로 만들어놓은 라이브러리

## 2. JSTL 제공 태그 종류

### 1) Core 태그

* 변수 선언, 조건문/반복문, URL 처리
* 접두어 : c

### 2) Formatting 태그

* 숫자, 날짜, 시간 포맷 지정
* 접두어 : fmt

### 3) XML태그

* XML 파싱
* 접두어 : x

### 4) Function 태그

### 5) SQL 태그

## 3. 코어(Core)태그

### 1) 변수선언, 조건문, 반복문 등을 대체하는 태그 제공

#### set 

* EL에서 사용할 변수 설정
* setAttribute() 메서드와 동일 기능

#### remove

* 설정한 변수 제거
* removeAttribute() 메서드와 동일 기능

#### if

* 단일 조건문 처리
* else문 없음

#### choose

* 다중 조건 처리
* when ~ otherwise 태그가 하위에 있음

#### forEach

* 반목문 처리 

#### forTokens

* 구분자로 분리된 각각의 토큰 처리할 때 사용
* StringTokenizer 클래스와 동일 기능

#### import
#### redirect

* sendRedirect() 메서드 동일 기능

#### url
#### out
#### catch

## 4. ```<c:set>``` 태그

### 1) EL에서 사용할 변수나 자바빈즈를 생성할 때 사용

```html
    <c:set var="변수명" value="값" scope="영역" />
    <c:set var="" scope=""> value 속성에 들어갈 값 </c:set>
```

### 2) 속성

* var : 변수명을 설정함
* value : 변수에 할당할 값
* scope : 변수를 생성할 영역을 지정함,page가 기본값

```html
<!--  태그 라이브러리 URI 식별자 -->
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>	
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSTL - set</title>
</head>
<body>
	<!-- 변수 선언 -->
	<c:set var="directVar" value="100" />
		
	<h4>EL 이용해 변수 출력</h4>
	<ul>
		<li>directVar : ${pageScope.directVar}</li>
	</ul>
</body>
```

![alt](/assets/images/post/jsp/116.png)


```jsp
    <c:set target="자바빈" property="변수 값" />
```

### target

* 자바빈즈를 설정함

### property

* 자바빈즈의 속성, 즉 멤버변수 값 지정함

```html
<h4>자바빈즈 생성2 - target, property 사용</h4>
	<c:set var="personVar2" value="<%= new Person() %>" scope="request" />
	<c:set target="${personVar2 }" property="name" value="이방원" />
	<c:set target="${personVar2}" property="age" value="30" />
	<ul>
		<li>이름 : ${personVar2.name }</li>
		<li>나이 : ${requestScope.personVar2.age }</li>
	</ul>
```

![alt](/assets/images/post/jsp/120.png)

## 5. ```<c:remove>```태그

* <c:set> 태그로 설정한 변수를 제거할 때 사용

```html
    <c:remove var="변수명" scope="영역" />
```

### var 

* 삭제할 변수명 설정

### scope 

* 삭제할 변수의 영역을 지정함.
* 지정하지 않으면 모든 영역의 변수가 삭제됨.

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!-- 변수 선언 -->
<c:set var="scopeVar" value="PageValue" />
<c:set var="scopeVar" value="RequestValue" scope="request" />
<c:set var="scopeVar" value="SessionValue" scope="session"/>
<c:set var="scopeVar" value="ApplicationValue" scope="application"/>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSTL - remove</title>
</head>
<body>
	<h4>출력하기</h4>
	<ul>
		<li>scopeVar : ${scopeVar }</li> 
		<!-- 영역을 지정하지 않으면 가장 좁은 영역인 page 영역이 지정 -->
		
		<li>requestScope.scopeVar : ${requestScope.scopeVar }</li>
		<li>sessionScope.scopeVar : ${sessionScope.scopeVar } </li>
		<li>applicationScope.scopeVar : ${applicationScope.scopeVar }</li>
	</ul>
	
	<h4>session 영역에서 삭제하기</h4>
	<c:remove var="scopeVar" scope="session" />
	<ul>
		<li>sessionScope.scopeVar : ${sessionScope.scopeVar } </li>
	</ul>
	
	<h4>scope 지정없이 삭제하기</h4>
	<c:remove var="scopeVar"/>
	<ul>
		<li>scopeVar : ${scopeVar }</li> 		
		<li>requestScope.scopeVar : ${requestScope.scopeVar }</li>
		<li>sessionScope.scopeVar : ${sessionScope.scopeVar } </li>
		<li>applicationScope.scopeVar : ${applicationScope.scopeVar }</li>
	</ul>
</body>
</html>
```

![alt](/assets/images/post/jsp/121.png)

## 6. ```<c:if>``` 태그

* 자바의 if와 동일

```jsp
    <c:if test="조건" var="변수명" scope="영역" >
        조건이 true일 때 출력할 문장
    </c:if>
```

```html
<c:set var="id" value="bob" scope="page" />
<c:set var="name" value="${'정원영' }" />
<c:set var="number" value="100"/>
<c:set var="string" value="100"/>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSTL - if</title>
</head>
<body>
	<c:if test="${true }">	<!-- 조건식이 true이므로 항상 참임 -->
		<h4>항상 참입니다.</h4>
	</c:if>
	
	<c:if test=" ${true } " var="result">
		<h4>EL 양쪽에 빈 공백이 있는 경우 </h4> <!--false-->
	</c:if>
	result : ${result }<br/>
	
	<c:if test="${13==13 }" >	<!-- 조건식에 비교 연산자를 사용 -->
		<h4>두 값은 같습니다.</h4>
	</c:if>
	
	<c:if test="${13 !=13 }">
		<h4>두 값은 같지 않습니다.</h4>
	</c:if>
	
	<c:if test="${(id=='bob') && (name=='정원영')}">
		<h4> 아이디는 ${id } 이름은 ${name }입니다.</h4>
	</c:if>
	
	<h4>JSTL의 if 태그로 짝수/홀수 판단하기</h4>
	<c:if test="${number mod 2 eq 0 }" var="result">
		<h4>${number }는 짝수 입니다.</h4>
	</c:if>
	result : ${result }<br>
	
	<h4>문자열 비교와 else 구문처럼 사용하기 </h4>
	<c:if test="${string eq 'Java' }" var="result2">
		출력되지 않음 <br>
	</c:if>
	<c:if test="${not result2 }">
		'Java'와 string은 같지 않습니다.<br>
	</c:if>
	
	<h4>조건식 주의사항</h4>
	<c:if test="bob" var="result3">
		EL이 아닌 일반 값이 오면 무조건 false를 반환함
	</c:if>
	result3 : ${result3 } <br>
	
	<c:if test="true" var="result4">
		EL이 아닌 일반 값으로 true가 사용되는 것은 예외임<br>
	</c:if>
	result4 : ${result4 } <br>
</body>
```

![alt](/assets/images/post/jsp/122.png)

## 7. ```<c:choose>,<c:when>,<c:otherwise>``` 태그

* switch문의 기능을 수행함
* 다중 조건을 통해 판단해야 할때 사용
* 태그 형식 

```html
<c:choose>
	<c:when test="조건식1">조건식1을 만족하면 경우</c:when> --> if 
	<c:when test="조건식2">조건식2를 만족하는 경우</c:when> --> else if
    ...
	<c:otherwise>아무 조건도 만족하지 않는 경우</c:otherwise> --> else
</c:choose>
```

* choose.jsp

```html
<body>
	<!-- 변수 선언 -->
	<c:set var="number" value="100" />
	
	<h4>choose 태그로 홀짝 판단하기</h4>
	<c:choose>
		<c:when test="${number mod 2 eq 0 }">
			${number }는 짝수입니다.
		</c:when>
		<c:otherwise>
			${number }는 홀수입니다.
		</c:otherwise>
	</c:choose>
	
	<h4>국, 영, 수 점수를 입력하면 평균을 내어 학점 출력</h4>
	<form action="#">
		국어 : <input type="text" name="kor"  /><br>
		영어 : <input type="text" name="eng"  /><br>
		수학 : <input type="text" name="mat"  /><br>
		<input type="submit" value="학점 구하기" />
	</form>
	
	<!-- 각 과목 점수 입력 체크 -->
	<c:if test="${ not (empty param.kor or empty param.eng or 
                                                empty param.mat) }">
		<!-- 평균계산 -->
		<c:set var="avg" value="${(param.kor+param.eng+param.mat)/3}" />
		평균 점수는 ${avg }으로 
		
		<!-- 학점 출력 -->
		<c:choose>
			<c:when test="${avg >=90 }">A 학점</c:when>
			<c:when test="${avg >=80 }">B 학점</c:when>
			<c:when test="${avg ge 70 }">C 학점</c:when>
			<c:when test="${avg >=60 }">D 학점</c:when>
			<c:otherwise>F 학점</c:otherwise>
		</c:choose>
	</c:if>
</body>
```

![alt](/assets/images/post/jsp/123.png)
![alt](/assets/images/post/jsp/124.png)
