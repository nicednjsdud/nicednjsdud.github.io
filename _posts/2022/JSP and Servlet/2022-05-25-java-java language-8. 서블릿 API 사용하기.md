---
title: JSP 8. 서블릿 API 사용하기 (Servlet) 
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
last_modified_at: '2022-05-25 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

서블릿 API 사용하기
====================

![alt](/assets/images/post/jsp/42.png)

## 포워드 기능

### 1) 하나의 서블릿에서 다른 서블릿이나 JSP와 연동하는 방법

* request에 대한 추가 작업을 다른 서블릿에게 수행하게 함
* request에 포함된 정보를 다른 서블릿이나 JSP와 공유함
* request에 정보를 포함시켜 다른 서블릿에 전달할 수 있음

### 2) 방법

#### redirect를 이용한 포워딩

* HttpServletResponse 객체의 sendRedirect() 이용
* 서블릿의 요청이 웹 브라우저를 거쳐 재요청하는 방식


##### FirestServlet

```java
package kr.co.ezenac.redirect;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/first")
public class FirstServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		response.sendRedirect("second");	// 웹 브라우저에게 다른 서블릿인 second로 재요청함
	}
}
```

##### SecondServlet

```java
package kr.co.ezenac.redirect;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/second")
public class SecondServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		out.print("<html><body>");
		out.print("sendRedirect를 이용한 redirect 실행!");
		out.print("</html></body>");
	}
}
```

![alt](/assets/images/post/jsp/43.png)


##### 다른 서블릿에 데이터 전달하기

* GET 방식
* FirstServlet

```java
    // GET 방식 이용해 이름, 값 쌍으로 데이터를 다른 서블릿으로 전달함.
		response.sendRedirect("second4?name=lee");
```

* SecondServlet

```java
// name으로 이전 서블릿에서 전달된 lee 받음
		String name = request.getParameter("name");
		
		out.print("<html><body>");
		out.print("이름 : "+name);
		out.print("</html></body>");
```

![alt](/assets/images/post/jsp/46.png)


#### refresh를 이용한 포워딩

* HttpServletResponse 객체의 addHeader() 메서드를 이용

```java
 response.addHeader("Refresh", 경과시간(초); url=요청할 서블릿 or JSP)
```

* 웹 브라우저를 거쳐서 요청을 수행

##### FirstServlet

```java
import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/first2")
public class FirstServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		// 웹 브라우저에게 2초 후 다른 서블릿인 second2로 재요청함
		response.addHeader("Refresh", "2;url=second2");
	}
}
```

##### SecondServlet

```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/second2")
public class SecondServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		out.print("<html><body>");
		out.print("refresh를 이용한 redirect 실행!");
		out.print("</html></body>");
	}
}
```

![alt](/assets/images/post/jsp/44.png)

#### location 방법

* 자바스크립트 location 객체의 href 속성을 이용
* 자바스크립트에서 재요청하는 방식
* 형식 : location.href = '요청할 서블릿 or JSP'

##### firstServlet

```java
@WebServlet("/first3")
public class FirstServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		// 자바스크립트의 location의 href 속성에 서블릿 second3을 설정해 재요청함
		out.print("<script>");
		out.print("location.href='second3' ");
		out.print("</script>");
		
	}
}
```

![alt](/assets/images/post/jsp/45.png)

#### dispatch 벙법

* 일반적으로 포워딩 기능을 지칭
* 서블릿이 직접 요청하는 방법 
* 클라이언트의 브라우저를 거치지 않고 서버에서 포워딩이 진행
* 모델2나 스프링 프레임워크에서 포워딩 시 사용
* RequestDispatcher 클래스의 forward() 메서드를 이용

##### FirstServlet

```java
        // dispatch 방법을 이용해 second5로 전달함
		// get방식으로 데이터를 전달함
		RequestDispatcher dispatch = request.getRequestDispatcher("second5?name=lee2");
		dispatch.forward(request, response);
```

![alt](/assets/images/post/jsp/46.png)
