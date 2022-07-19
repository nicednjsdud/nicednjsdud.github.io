---
title: (Spring) 5. Spring MVC 이란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Spring MVC
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# MVC 패턴의 개념

## 1. MVC패턴의 개념

### 1) 모델-뷰-컨트롤러는 아키텍쳐 패턴

### 2) 주 목적은 Bussiness logic과 Persentation logic을 분리위함.

### 3)

- Model : 애플리케이션의 정보 (데이터, Business logic)
- View : 사용자에게 제공할 화면 (Persentation logic)
- Controller : Model과 View사이의 상호 작용을 관리

![alt](/assets/images/post/spring/9.png)

## 2. MVC 컴포넌트 역할

### 1) 모델(Model) 컴포넌트

- 데이터나 저장소(DB)와 연동하여 사용자가 입력한 데이터나 사용자에게  
  출력할 데이터를 다루는 일을 함.
- 데이터의 추가, 변경, 삭제
- DAO 클래스, Service 클래스에 해당

### 2) 뷰(View) 컴포넌트

- 모델이 처리한 데이터나 그 작업 결과를 가지고 사용자에게 출력할 화면을  
  만드는 일을 함.
- HTML, CSS, JavaScript, JSP를 사용하여 웹 브라우저가 출력할 UI를 만듦

### 3) 컨트롤러(Controller) 컴포넌트

- 클라이언트의 요청을 받았을 때 그 요청에 대해 실제 업무를 수행하는 모델  
  컴포넌트를 호출하는 일을 함
- 클라이언트가 보낸 데이터가있다면, 모델을 호출할 때 전달하기 쉽게 데이터를  
  적절히 가공하는 일을 함.
- 모델이 업무 수행을 완료하면, 그 결과를 가지고 화면을 생성하도록 뷰에게 전달

#### Servlet(모델2 아키텍쳐), JSP(모델1 아키텍쳐)

- 서블릿 컨테이너 (톰캣 서버)는 URL을 확인하여 그 요청을 처리할 서블릿을  
  찾아서 실행함.

## 3. Front Controller 패턴

![alt](/assets/images/post/spring/8.png)

- Front Controller는 클라이언트가 보낸 요청을 받아서 공통적인 작업을 먼저 수행

  - 인증, 권한 체크

- 적절한 세부 Controller에게 작업을 위임
- 각각의 애플리케이션 Controller는 뷰를 선택해서 최종 결과를 생성하는 작업

## 4. Spring MVC 특징

- Spring은 DI나 AOP 같은 기능 + 서블릿 기반의 웹 개발을 위한 MVC 프레임워크 제공
- 모델2 아키텍쳐 + Front Controller 패턴을 프레임워크 차원에서 제공
- Front Controller 역할을 하는 DispatcherServlet 클래스를 맨 앞단에 놓고,  
  서버로 들어오는 모든요청을 받아서 처리하도록 구성

### 1) DispatcherServlet 클래스

- Front Controller 패턴 적용
- web.xml에 설정
- 클라이언트로부터의 모든 요청을 전달 받음

## 5. Spring MVC 수행 과정

![alt](/assets/images/post/spring/10.png)

1. 브라우저가 DispatcherServlet에 URL로 접근하여 해당 정보를 요청함.
2. 핸들러 매핑에게 해당 요청에 대해 매핑된 컨트롤러가 있는지 요청함
3. 매핑된 컨트롤러에 대해 처리를 요청함
4. 컨트롤러가 클라이언트의 요청을 처리한 결과와 View 이름을 ModelandView에  
   저장해서 DispatcherServlet으로 반환
5. DispatcherServlet에서는 컨트롤러에서 보내온 View이름을 ViewResolver로  
   보내 해당 View를 요청함.
6. ViewResolver는 요청한 View를 보냄
7. View의 처리결과를 DispatcherServlet으로 보냄
8. DispatcherServlet은 최종 결과를 브라우저로 전송함.

## 6. Spring MVC 주요 구성 요소

### 1) DispatcherServlet

- 클라이언트의 요청을 받아서 Controller에게 클라이언트의 요청을 전달하고,  
  리턴한 결과값을 View에게 전달하여 알맞은 응답을 생성

### 2) HandlerMapping

- URL과 요청 정보를 기준으로 어떤 핸들러 객체를 사용할지 결정하는 객체

### 3) Controller

- 클라이언트의 요청을 처리한 뒤, Model을 호출하고 그 결과를 DispatcherServelt  
  에게 알려줌.

### 4) ModelAndView

- Controller가 처리한 데이터 및 화면에 대한 정보를 보유한 객체

### 5) ViewResolver

- Controller가 리턴한 뷰 이름을 기반으로 Controller 처리 결과를 생성할 뷰를  
  결정

### 6) View

- Controller의 처리 결과 화면에 대한 정보를 보유한 객체
