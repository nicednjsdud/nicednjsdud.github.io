---
title: JSP 9. 내장 객체 영역 (Scope)  
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JSP and Servlet
description: JSP
tag : JSP
article_tag1: JSP
article_section: JSP
meta_keywords: java,java JSP, JDBC
last_modified_at: '2022-05-26 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

내장 객체 영역(Scope)
=====================

## 내장 객체의 영역

![alt](/assets/images/post/jsp/51.png)

### 1) 각 객체가 저장되는 메모리의 유효기간.

### 2) jsp와 같은 웹 어플리케이션은 페이지 단위로 구성됨
* A 페이지에서 선언한 변수를 B 페이지로 이동한 후에도 접근여부 다름.

### 3) 총 4가지

![alt](/assets/images/post/jsp/53.png)

#### page 영역

* 동일한 페이지에서만 공유됨. 페이지를 벗어나면 소멸됨.
* pageContext 객체를 사용

#### request 영역

* 하나의 요청에 의해 호출된 페이지와 포워드(요청 전달)된 페이지까지 공유됨
* request 객체를 사용

#### session 영역

* 클라이언트가 처음 접속한 후 웹 브라우저를 닫을 때 까지 공유됨
* session 객체를 사용

#### application 영역

* 한 번 저장되면 웹 애플리케이션이 종료될 떄까지 유지됨.
* application 객체를 사용

### 4) 주요 메서드 

```java
    void setAttribute(String name, Object value)
```

* 각 영역에 속성을 저장함

```java
    Object getAtrribute(String name)
```

* 영역에 저장된 속성값 얻어옴

```java
    void removeAttribute(String name)
```

* 영역에 저장된 속성을 삭제함.

## page 영역

* 기본적으로 클라이언트 요청을 처리하는 데 관여하는 JSP 페이지마다 하나씩  
  생성됨.
* 각 jsp 페이지는 page 영역을 사용하기 위한 pageContext 객체를 할당받게 됨.
* page 영역에 속성 저장
	* pageContext.setAtrribute(속성명, 값);
* page 영역에 속성 읽기
	* pageContext.getAtrribute();

* pageContext 객체에 저장된 정보는 해당 페이지에서만 사용 가능,  
  페이지를 벗어나면 소멸됨.
* include 지시어로 포함한 파일은 같은 페이지므로 page 영역이 공유됨.

```jsp
<%@page import="kr.co.ezenac.dto.Person"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	// pageContext객체를 통해 page 영역에 숙성값을 저장함.
	pageContext.setAttribute("pageInteger", 1000);
	pageContext.setAttribute("pageString", "페이지 영역에 문자열");
	pageContext.setAttribute("pagePerson", new Person("이순신", 30));
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>page 영역</title>
</head>
<body>
	<h2>page 영역의 속성값 읽기</h2>
	<%
		// 속성읽기
		int pInteger =(Integer) (pageContext.getAttribute("pageInteger"));
		String pString = pageContext.getAttribute("pageString").toString();
		Person pPerson = (Person)(pageContext.getAttribute("pagePerson"));
		
	%>
	<ul>
		<li>Integer 객체 : <%= pInteger %></li>
		<li>String 객체 : <%=pString %></li>
		<li>Person 객체 : <%=pPerson.getName() %>,<%=pPerson.getAge() %></li>
	</ul>
</body>
</html>
```

![alt](/assets/images/post/jsp/52.png)

## request 영역

* 클라이언트가 요청을 할 때마다 새로운 request 객체가 생성
* request 영역은 같은 요청을 처리하는 데 사용되는 모든 JSP가 공유
	* request 영역에 저장딘 정보는 현재 페이지와 포워드된 페이지까지 공유
	* 페이지 이동 시에는 소멸되어 사용할수 없게 됨.
* 하나의 요청에 대한 응답이 완료될 때 소멸하게 됨.

### 1) requestMain.jsp

```java
<%
	request.setAttribute("requestString", "request 영역의 문자열");
	request.setAttribute("requestPerson", new Person("이방원",32));
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>request 영역</title>
</head>
<body>
	<h2>request 영역의 속성값 삭제하기</h2>
	<%
		request.removeAttribute("requestString");
		request.removeAttribute("requestPerson1");	// 에러 없음
	%>
	
	<h2>request 영역의 속성값 읽기</h2>
	<%
		Person rPerson = (Person)(request.getAttribute("requestPerson"));
	%>
	<ul>
		<li>String 객체 : <%= request.getAttribute("requestString") %></li>
		<li>Person 객체 : <%= rPerson.getName() %>,<%=rPerson.getAge() %></li>
	</ul>
	
	<h2>포워드된 페이지에서 request 영역 속성값 읽기</h2>
	<%
		request.getRequestDispatcher("requestForwad.jsp?paramBob=BoB&paramAdress=GangNam")
		.forward(request, response);
	%>
	
	
</body>
```

![alt](/assets/images/post/jsp/55.png)

### requestFoward.jsp (포워딩)

```jsp
	<%@page import="kr.co.ezenac.dto.Person"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>request 영역</title>
</head>
<body>
	<h2>포워드로 전달된 페이지</h2>
	<h4>requestMain.jsp 파일의 리쿼스트 영역 속성 읽기</h4>
	<%
		Person pPerson =(Person)(request.getAttribute("requestPerson"));
	%>
	<ul>
		<li>String 객체 : <%=request.getAttribute("requestString") %></li>
		<li>Person 객체 : <%= pPerson.getName() %>,<%= pPerson.getAge() %></li>
	</ul>
	
	<h4>매개변수로 전달된 값 출력하기</h4>
	<%
		request.setCharacterEncoding("utf-8");
		out.print(request.getParameter("paramBob"));
		out.print("<br>");
		out.print(request.getParameter("paramAdress"));
	%>
</body>
</html>
```

![alt](/assets/images/post/jsp/54.png)

## session 영역

* 클라이언트가 웹 브라우저를 최초로 열고 난 후 닫을 때까지 요청되는 모든 페이지는  
  session 객체를 공유할 수 있음.

### 클라이언트가 서버에 접속해 있는 상태 혹은 단위 

* 주로 회원인증 후 로그인 상태를 유지하는 처리에 사용됨
* 웹 브라우저를 닫으면 자동으로 로그아웃이 됨

### 1) sessionMain.jsp

```jsp
	<%
		ArrayList<String> lists0 = new ArrayList<>();
		lists0.add("이젠");
		lists0.add("개발자");
		
		session.setAttribute("lists", lists0);
	%>
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<meta name ="viewport" content="width=device-width, init-scale=1.1">
	<title>session 영역</title>
	</head>
	<body>
		<h2>페이지 이동 후 session 영역의 속성 읽기</h2>
		<a href = "sessionLocation.jsp">sessionLocation.jsp 바로가기</a>
	</body>
```

![alt](/assets/images/post/jsp/57.png)

### 2) sessionLocation.jsp

```jsp
	<body>
		<h2>페이지 이동 후 session 영역의 속성 읽기2</h2>
		<%
			ArrayList<String> lists =(ArrayList<String>)(session.getAttribute("lists"));
			for(String str : lists)
				out.print(str + "<br/>");
		%>
	</body>
```

![alt](/assets/images/post/jsp/56.png)

## application 영역

* 웹 애플리케이션은 단 하나의 application 객체만 생성함
* 클라이언트가 요청하는 모든 페이지가 application 객체를 공유하게됨.
* 웹 서버를 시작할 때 만들어지며, 웹서버가 종료될 때 삭제됨.
* application 영역에 한번 저장된 정보는 페이지를 이동하거나,   
  웹브라우저를 닫았다가 새롭게 접속해도 삭제되지 않음


### 1) applicationMain.jsp

 ```jsp
	<title>application 영역</title>
	</head>
	<body>
		<h2>application 영역의 공유</h2>
		<%
			Map<String, Person> maps = new HashMap<>();
			maps.put("actor1", new Person("정도전",30));
			maps.put("actor2",new Person("이도",20));
			
			application.setAttribute("maps", maps);
		%>
		application 영역에 속성이 저장되었습니다.
	</body>
 ```

![alt](/assets/images/post/jsp/58.png)

### 2) applicationResult.jsp

```jsp
<title>application 영역</title>
</head>
<body>
	<h2>application 영역의 속성 읽기</h2>
	<%
		Map<String,Person> maps =(Map<String,Person>)(application.getAttribute("maps"));
		Set<String> keys = maps.keySet();
		for(String key: keys){
			Person person = maps.get(key);
			out.print(String.format("이름 : %s, 나이 : %d<br/>",person.getName(),person.getAge()));
		}
		
	%>
</body>
```

![alt](/assets/images/post/jsp/59.png)
