---
title: JSP 6. JSP 기본 (JSP) 
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
last_modified_at: '2022-05-23 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JSP 기본
==========

## 지시어 (Directive)

* JSP 페이지를 자바(서블릿)코드로 변환하는데 필요한 정보를 JSP 엔진에 알려줌
* 주로 스크립트 언어, 인코딩 방식 설정

```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

    <%@ 지시어종류 속성1="값1" 속성2="값2; ..." %>
```

### 1) page 지시어 

* JSP 페이지에 대한 정보 설정

#### import

* 페이지에서 사용할 자바 패키지와 클래스를 지정함

```jsp
<%@page import="java.text.SimpleDateFormat"%>
<%@page import="java.util.Date"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>page 지시어 - import 속성</title>
</head>
<body>
	<%
		Date today = new Date();
		SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
		String todayStr = dateFormat.format(today);
		out.println("오늘 날짜 : "+todayStr);
	%>	
</body>
...
```

![alt](/assets/images/post/jsp/22.png)

#### errorPage

* 해당 페이지에서 에러가 발생했을 때 에러 발생여부를 보여줄 페이지를 지정함

```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="isErrorpage.jsp"%>
```

#### isErrorPage

* 해당 페이지에서 에러를 처리할지 여부를 지정함

```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="true" %> <!-- errorpage="true"-->
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>page 지시어 - errorPage,</title>
</head>
<body>
	<img alt="에러이미지" src="image/error-page.gif"/>
	<h2>서비스 중 일시적인 오류가 발생하였습니다</h2>
	<h2>잠시 후 다시 시도해 보세요.</h2>
```

![alt](/assets/images/post/jsp/23.png)

#### trimDirectiveWhitespaces

* page 지시어로 생긴 불필요한 공백 제거

#### buffer, autoFlush

* 출력할 내용을 버퍼에 저장했다가 일정량이 되었을 때 전송하게 됨.
* 버퍼를 사용함으로써 포워드(forward, 페이지전달)와 에러 페이지 처리 가능
* JSP가 생성한 결과 일단 버퍼에 저장됨.
* buffer 기본값은 8kb 
* autoFlush 기본값은 true : 버퍼가 채워지면 자동으로 플러시함.
    - false : 버퍼가 채워지면 예외를 발생시킴
    - 플러시(flush) : 버퍼 안의 데이터를 목적지로 전송하고 버퍼를 비우는 작업을 말함

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" buffer="8kb" autoFlush="true" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>page 지시어 - buffer autoFlush</title>
</head>
<body>
	<%
		for(int i=1;i<=100;i++){
			out.print("abcdefgh12345");
		}
	%>
</body>
</html>
```

![alt](/assets/images/post/jsp/24.png)

### 2) include 지시어 

* 외부 파일을 현재 JSP 페이지에 포함 시키면 '파일의 내용 그대로를 문서에 삽입' 한 후  
  '컴파일'이 진행됨.
    * => 하나의 페이지가 됨.
#### File

```jsp
    <title>포함될 파일</title>
</head>
<body>
	<%
		LocalDate today = LocalDate.now();	// 오늘 날짜
		LocalDate tomorrow = LocalDate.now().plusDays(1);	// 내일 날짜
	%>
</body>
```

#### Main

```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ include file="includeFile.jsp"  %> <!-- 다른JSP 파일 포함 -->
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name ="viewport" content="width=device-width, init-scale=1.1">
<title>include 지시어</title>
</head>
<body>
	<%
		out.println("오늘 날짜 : "+ today);
		out.println("<br/>");
		out.println("내일 날짜 : "+tomorrow);
	%>
</body>
</html>
```

![alt](/assets/images/post/jsp/25.png)

### 3) taglib 지시어 

* 표현 언어(EL)에서 사용할 자바 클래스, JSTL을 선언

## 스크립트 요소 (Script Elements)

### 1) jsp에서 자바 코드를 직접 작성할 수 있게 해줌.

* 선언부, 스크립틀릿, 표현식

### 2) 선언부 (Declaration)

```jsp
    <%! 변수,메서드 선언 %>
```

* 스클립틀릿이나 표현식에서 사용할 멤버변수나 메서드 선언함

### 3) 스크립틀릿 (Scriptlet)

```JSP
    <% 자바 코드 %>
```

* JSP 페이지가 요청을 받았을 때 실행돼야 할 자바 코드를 작성하는 영역임
* 서블릿으로 변환시 _jspService()메서드 내부에 그대로 기술됨

### 4) 표현식 (Expression)

```jsp
    <% 자바 표현식 %>
```

* 변수의 값을 웹 브라우저 화면에 출력할 때 사용함.