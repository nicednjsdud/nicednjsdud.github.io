---
title: JSP 11. 세션
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
last_modified_at: '2022-05-30 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

세션
====

## 테이블 및 시퀀스 생성

### 1) 게시판에 글을 작성하려면 회원 인증이 필요

* 회원 정보 저장하는 member 테이블

![alt](/assets/images/post/jsp/77.png)
![alt](/assets/images/post/jsp/78.png)

* 게시글을 저장하는 board 테이블

### 2) 테이블 생성

## 세션(Session)

### 1) 서로 관련된 요청들을 하나로 묶은 것 - 쿠키를 이용

```
    a collection of related HTTP transactions
```

* browser마다 개별 저장소(Session 객체)를 서버에서 제공

```
    made by one browser to one server
```

### 2)

* 웹 페이지들 사이의 공유 정보를 서버의 메모리에 저장해 놓고 사용하는 방법

### 3) 목적

* 클라이언트가 서버에 접속해 있는동안 그상태를 유지하는 것

## 세션의 특징

* 정보가 서버의 메모리에 저장
* 쿠키보다 보안에 유리
* 서버에 부하를 줄 수 있음
* 브라우저(사용자)당 한개의 세션(세션id)이 생성됨.
* 세션은 유효 시간을 가짐 (기본 유효 시간은 30분)
* 로그인 상태 유지 기능이나 쇼핑몰의 장바구니 담기 기능 등에 주로 사용됨.

## 세션 기능 실행 과정

1. 브라우저로 사이트 접속함.
2. 서버는 접속한 브라우저에 대한 세션 객체를 생성함
3. 서버는 생성된 세션 id를 클라이언트 브라우저에 응답함.
    * 세션 아이디를 값으로 받는 jsessionId 쿠키를 응답 헤더에 담아 웹 브라우저에 보냄

4. 브라우저는 서버로부터 받은 세션id를 브라우저가 사용하는 메모리의 쿠키에 저장함.
    * 쿠키 이름 - jsessionId
    * 톰캣 컨테이너에서 새로운 웹 브라우저가 접속을하면 세션을 유지하기 위해서   
      자동으로 생성해줌.
    * 이 jsessionId는 요청을 보낸 웹 브러우저가 현재 연결되어 있는지(세션이 살아있는지)  
      확인하는데 이용됨. 

5. 브라우저가 재접속하면 브라우저는 쿠키에 저장된 세션 id를 서버에 전달함.
    * 재 요청시마다 jsessionId를 요청 헤더에 추가하여 보냄.
6. 서버는 전송된 세션 id를 이용해 해당 세션에 접근하여 작업을 수행함.
    * 요청 헤더에 포함된 jsessionId로 해당 요청이 기존 세션에서 이어진 것임을 알게됨.

## 세션 API

### 1) 세션 얻는 방법

#### HttpServletRequest getSession() 메서드 호출

* 기존의 세션 객체가 존재하면 반환하고, 없으면 새로 생성

### 2) 
#### getAttribute(String name)

#### getId()

#### getMaxInactiveInterval()  

* 세션 유지시간을 int타입으로 반환

#### getCreationTime()

* 1970년 1월 1일 0시 0분 0초를 기준으로 현재 세션이 생성된 시간까지  
  경과한 시간을 계산하여 1/1000초 값 반환

#### invalidate()  

* 현재 생성된 세션 소멸함.

#### removeAttribute(String name)

#### setAttribute(String name, Object value)   

* 세션 속성 이름이 name인 속성 값으로 value를 할당함

#### setMaxInactiveInterval(int interval)

* 세션 유지시간을 초단위로 설정함.

```java
package kr.co.ezenac.session;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/sess3")
public class SessionTest3 extends HttpServlet {
	@SuppressWarnings("deprecation")
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
                                                    throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		// 최초 요청시 세션 객체를 
		HttpSession session = request.getSession();
		out.print("세션 아이디: "+session.getId()+"<br/>");
		out.print("최초 세션 생성 시각: "+new Date(session.getCreationTime())+"<br>");
		out.print("최초 세션 접근 시각 : "+new Date(session.getLastAccessedTime())+"<br>");
		out.print("톰캣 기본 세션 유효 시간 : "+session.getMaxInactiveInterval()+"<br>");
		
		// 세션의 유효 시간을 5초로 설정
		session.setMaxInactiveInterval(5);	// 5초
		// 유효 시간 재설정한 후 세션 유효 시간 출력
		out.print("세션 유효시간 : "+session.getMaxInactiveInterval()+"<br>");
		
		// 최초 생성된 세션인지 판별
		if(session.isNew()) {
			out.print("새 세션이 만들어졌습니다.");
		}
		
		// 생성된 세션 객체를 강제로 삭제
		session.invalidate();
	}
}

```

![alt](/assets/images/post/jsp/79.png)

## 쿠키 vs 세션

|----|		쿠키		|		세션		|
|--------|----------|---------------|
|저장위치/형식|	클라이언트 PC에 text에 저장됨 | 웹서버에 Object 타입으로 저장됨|
|보안| 보안에 취약함| 서버에 저장되므로 보안에 안전함|
|자원/속도|서버자원을 사용하지 않으므로 세션보다 빠름| 서버자원을 사용하므로 쿠키보다 느림|
|용량|용량제한이 있음|서버가 허용하는 한 제한이 없음|
|유지시간|쿠키 생성시 설정함| 서버의 web.xml에서 설정함.|
|설정| 설정된 시간이 경과되면 무조건 삭제| 설정된 시간내라도 동작이 있다면 삭제되지 않고 유지됨|