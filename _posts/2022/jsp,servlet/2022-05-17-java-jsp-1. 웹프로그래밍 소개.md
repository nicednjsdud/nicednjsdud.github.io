---
title: JSP 1. 웹프로그래밍 소개  
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
last_modified_at: '2022-05-17 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

웹 프로그래밍 소개
================

## 용어

### 1) web.xml (배포 서술자)

* 웹 어플리케이션의 환경설정 정보를 담은 파일.

```
    - 서블릿 설정, 필터 설정, 파일 목록, 오류 페이지 처리 설정 등
```

* WAS (Web Application Server)가 처음 구동될 때 이 파일을 읽어  
  설정 내용을 톰캣에 적용하게 됨.

### 2) 웹 서버(Server Container)

![alt](/assets/images/post/jsp/3.png)

* 사용자로부터 HTTP를 통해 요청을 받거나, 웹 컨테이너가 전달해준 결과물을  
  정적인 페이지로 생성하여 사용자에게 응답해주는 소프트웨어임.
* 웹 페이지는 주로 HTML, CSS, JS 등으로 구성됨.

### 3) 웹 컨테이너(Web Container)

* 웹 서버가 전송해준 요청을 기초로 동적인 페이지를 생성하여 웹서버에게 돌려줌
* 동적인 페이지라고 표현하는 이유

```
    - 사용자마다 다른 결과로 응답할수 있기 때문임.(Login)
```

### 4) WAS (Web Application Server)

* 웹 애플리케이션이 실행될 수 있는 환경 제공하는 소프트웨어
* 웹 서버와 웹 컨테이너를 포함한 개념임
* 톰캣, 웹로직, 웹스피어 등.

![alt](/assets/images/post/jsp/4.png)

### 5) HTTP (Hyper Text Transfer Protocol) / HTTPS

* www에서 웹 서버와 사용자 사이의 통신을 위해 사용하는 통신 프로토콜.
* 사용자가 요청하면 웹 서버가 응답하는 단순한 구조의 프로토콜

### 6) 프로토콜 (Protocol)

* 네트워크를 통해 컴퓨터들이 정보를 주고받는 절차 혹은 통신규약을 말함.
* 서로 다른 컴퓨터들이 대화하는데 필요한 공통 언어.
* HTTP도 프로토콜의 한 종류임
* FTP (File Transfer Prtocol), SMTP(Simple Mail Transfer Prtocol) 등.

### 7) 포트(port)

* 컴퓨터 사이에서 데이터를 주고받을 수 있는 통로.
* 인터넷에서 IP 주소를 통해 서버 컴퓨터 위치 파악함. 그런 다음에 그 컴퓨터  
  가 제공하는 특정 서비스는 포트 번호를 통해 알수 있음.
    * 모든 서비스는 IP 주소와 함께 포트 번호까지 지정해야 제대로 요청을 전달 할수있음.
* HTTP는 80번 포트, HTTPS는 443번 포트 등.

![alt](/assets/images/post/jsp/5.png)
![alt](/assets/images/post/jsp/6.png)

## 서블릿

### 1) 서버 측에서 실행되는 Servlet

* 클라이언트의 요청을 받으면 서버에서 처리한 후, 응답으로는 결과값 보내주는 구조임.

### 2) 주요 차이 비교

```
        서블릿                              JSP
----------------------------------------------------------------
- 자바 코드안에서 전체 HTML페이지를 생성   HTML 코드안에 필요한 부분만 자바코드를 
                                        스크립트 형태로 추가

- 변수 선언 및 초기화가 반드시 선행        내장 객체(자주 쓰이는 기능)로 제공

- 컨트롤러(Controller)를 만들때 사용     처리된결과를 보여주는 뷰(View)만들때 사용
```

![alt](/assets/images/post/jsp/7.png)
![alt](/assets/images/post/jsp/8.png)

## 웹 구동 방식 (Java 중심)

![alt](/assets/images/post/jsp/9.png)

