---
title: JSP 3. Servlet (Servlet) 
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
last_modified_at: '2022-05-20 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Servlet
===========

![alt](/assets/images/post/jsp/10.png)

## 서블릿

* JSP가 나오기 전, 자바로 웹 애플리케이션을 개발할 수 있도록 만든  기술이다.
* 서버 단에서 클라이언트의 요청을 받아서 처리한 후 응답하는 역할을 함.
* 클라이언트의 요청에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트이다. 

## 서블릿 특징

* 기존의 정적인 웹 프로그래밍의 문제점을 보완하여 동적인 여러 가지   
  기능을 제공함.
* 스레드 방식으로 실행됨.  **(Request, Response)**
* 자바로 만들어져 자바의 특징(OOP)을 가짐.
* 웹 브라우저에서 요청 시 기능을 수행함.
* HttpServlet 클래스를 상속 받음.
* 컨테이너에서 실행 

## 서블릿 API

```java
    (i)Servlet           (i)ServletConfig   i: interface
            \              /
            GenericServlet : 추상클래스
            HttpServlet : 클래스
```

### 1) HttpServlet

![alt](/assets/images/post/jsp/11.png)


* GenericServlet을 상속받아 HTTP 프로토콜을 사용하는 웹 브라우저  
  에서 서블릿 기능 수행함
* 웹 브라우저 기반 서비스를 제공하는 서블릿을 만들 떄 상속받아 사용함.
* 요청 시 service()가 호출되면 요청 방식에 따라 doGet()이나 doPost()  
가 차례대로 호출됨.

### 2) 서블릿 생명주기(Life Cycle) 메서드

* 서블릿 실행 단계마다 호출되어 기능을 수해오디는 콜백메서드

#### init()

* 초기화
* 서블릿 요청시 맨 처음 한번만 호출됨.
* 생략가능

#### doGet(), doPost()

* 서블릿 요청 시 매번 호출됨 
* 실제로 클라이언트가 요청하는 작업을 수행함
* 반드시 구현해야함.

#### Destroy()

* 서블릿이 메모리에서 소멸될 때 호출됨
* 마무리 작업을 주로 수행
* 생략 가능

## 서블릿 매핑 방법

* 각 프로젝트에 있는 web.xml에서 설정
* servlet 태그와 servlet-mapping 태그를 이용함
* 여러개의 서블릿 매핑 시에는 servlet 태그를 먼저 정의하고   
  servlet-mapping 태그를 정의함.

```xml
        ...
      </welcome-file-list>
  
  <servlet>
  	<servlet-name>ezenac</servlet-name>
  	<servlet-class>kr.co.ezenac.FirstServlet</servlet-class>
  </servlet>
                            <!-- 웹브라우저에서 요청하는 매핑이름 -->
  <servlet-mapping>
  	<servlet-name>ezenac</servlet-name>
  	<url-pattern>/first</url-pattern>
  </servlet-mapping>
  
</web-app>
```

![alt](/assets/images/post/jsp/12.png)

## 서블릿 매핑하기

```
http://주소:포트번호/프로젝트명(컨텍스트 이름)/패키지명이 포함된 클래스명

```

* 서블릿 클래스에 대응하는 서블릿 매핑 이름으로 요청함.

```
http://주소:포트번호/프로젝트명(컨텍스트 이름)/서블릿매핑이름

```

## 에너테이션을 이용한 서블릿 매핑

* web.xml에 여러 서블릿 매칭 설정 시 복잡해짐
* 서블릿 클래스에 직접 에너테이션을 설정하면 가독성이 좋아짐.
* @WebServlet을 이용해서 서블릿 매핑을 구현함.

```java
    @WebServlet("/서블릿 매핑이름")
```

