---
published: true
title: (10분 테크톡) (Spring) 18. Servlet vs Spring
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-04-28 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Servlet vs Spring

## 1. Servlet

- 웹 애플리케이션을 만들때 필요한 인터페이스

### 1) Spring Web MVC

- 스프링 모듈
- Web Service를 만든다.
- MVC 패턴을 사용해서 (Model View Controller)

## 2. Servlet은 왜 생겻을까?

### 1) 정적 데이터만 전달하는 Web Server

![alt](/assets/images/post/ComputerStudy/979.png)

### 2) 동적 데이터를 처리하는 CGI

- Common Gateway Interface

![alt](/assets/images/post/ComputerStudy/980.png)

- CGI : Web Server와 프로그램 사이의 규약

![alt](/assets/images/post/ComputerStudy/981.png)

- 하지만 CGI는 많은 사용자를 처리하기에는 무리

![alt](/assets/images/post/ComputerStudy/982.png)

### 3) CGI를 보완한 Servlet

- WebContainer : 요청이 들어오면 Thread를 생성하고 Servlet을 실행시킴
  - Servelt interface에 따라 Servlet을 관리

![alt](/assets/images/post/ComputerStudy/983.png)

## 2. Servlet의 생명 주기

### 1) Init

- Servlet Instance 생성 (initalize)

### 2) Service

- 실제 기능이 수행되는 곳
- abstract class HttpServlet extends Servlet
- HTTP Method(GET, POST, PUT, DELETE)에 따라 doGet(), doPost(), doDelete() 메서드를 호출
- doXXX() : 개발자가 구현

### 3) Destroy

- Servlet Instance가 사라진다.
- 보통 container가 종료되는 시점에 destroy() 호출
- 특정 servlet 로드/ 언로드 시에도 사용

### 4)

- 각메서드는 Servlet Container (Tomcat)이 호출해준다.

## 3. Servlet code

- Web.xml

```xml
  <wep-app>
    <servlet>
      <servlet-name>member</servlet-name>
      <servlet-class>servlets.MemberSerlvet</servlet-class>
    </servlet>
    <servlet-mapping>
      <servlet-name>member</servlet-name>
      <url-pattern>/member</url-pattern>
    </servlet-mapping>
  </wep-app>
```

- Web.xml(설정파일) Servlet Mapping
- WAS에게 Servlet 객체 - URL mapping 정보를 알려준다.

```java
  public class MemberServlet extends HTTPServlet{
    protected voi doPost(HttpServletRequest req,
              HttpServletResponse res) throws ServletException, IOException {

                String userName = request.getParameter("userName")
                String password = request.getParameter("password")

                String result = doSomething(userName, password);

                Stirng htmlResponse = "<html>"
                htmlResponse += "<h2>Result: " + result + "</h2>";
                htmlResponse += "<html>";

                PrintWriter writer = response.getWriter();
                writer.println(htmlResponse)
              }
  }
```

![alt](/assets/images/post/ComputerStudy/984.png)

## 4. Spring 에서는 Servlet을 어떻게 사용할까?

- Dispatcher Servlet

![alt](/assets/images/post/ComputerStudy/985.png)

- 모든 요청이 들어왔을때, Dispatcher Servlet으로 간다.

![alt](/assets/images/post/ComputerStudy/986.png)

- 요청에 따라 적절한 Controller을 사용
- 찾는 방법은 스프링 프레임워크에서 제공

![alt](/assets/images/post/ComputerStudy/987.png)

- HandlerMapping에서 찾은 Handler(Controller)의 메서드를 호출
- ModelAndView 형태로 바꿔줌
  - Data에 해당하는 Model, Data를 넘길 page에 해당하는 View
  - 보통 View의 논리적인 이름만 return해줌

![alt](/assets/images/post/ComputerStudy/988.png)

- View에 Model(data)를 포함시켜준다.

![alt](/assets/images/post/ComputerStudy/989.png)

- View의 이름으로 실제 View 객체를 생성

### 1) Dispatcher Servlet - Handler Mapping

- Spring Framework에서 제공하는 HandlerMapping
- 어떤 방식의 HandlerMapping을 사용할지 설정파일에 지정
- Servlet을 등록하면 그 Servlet이 사용할 설정파일이 자동으로 등록

#### 1-1) BeanNameHandlerMapping

- Bean 이름과 Url을 Mapping 하는 방식

## 출처

<a href="https://www.youtube.com/watch?v=y0xMXlOAfss">타미의 Servlet vs Spring</a>
