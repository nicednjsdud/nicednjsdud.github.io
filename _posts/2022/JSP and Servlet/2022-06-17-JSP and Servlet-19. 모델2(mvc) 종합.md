---
title: JSP 17. 모델 mvc 게시판 구현 설명(1)
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
last_modified_at: '2022-06-17 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델 2 (MVC) JSP board 구현 설명
============================

## 1. 웹 애플리케이션 모델

* 애플리케이션 개발시 일반적으로 많이 사용하는 표준하도니 소스 구조
* 모델의 종류에는 모델1과 모델2가 있음

![alt](/assets/images/post/ajax/15.png)
![alt](/assets/images/post/ajax/16.png)

## 2. MVC 디자인 패턴

* 일반 PC 프로그램 개발에 사용되는 디자인 패턴을 웹 애플리케이션에 도입한 것
* 각 기능 분리되어 있어 개발 및 유지보수가 상대적으로 편리함.

## 3. 구현 순서

1. 목록보기
2. 글쓰기
3. 상세보기
4. 파일 다운로드
5. 삭제하기
6. 수정하기

## 4. 게시판 구상

### 1) 비회원제

* 회원인증 없이 누구나 글을 작성할 수 있음
* 글쓰기 시 비밀번호 입력이 필수임
* 비밀번호를 통해 수정, 삭제가능

### 2) 자료실

* 글쓰기시 파일 첨부
* 파일 첨부시 정해진 용량 이상 업로드 금지
* 첨부된 파일 다운로드

### 3) 프로세스

```
        ---------------------------------------------------------
        |                                                       |
        |                                                       |
        \/                                                      |
    목록보기화면    ------------>    글쓰기 화면  ----------> 글쓰기 처리
    (ListController.java
        list.jsp)     글쓰기 클릭     (write.jsp)   (wirteController.java)

        |
        |
        |
제목클릭\/
                 수정 클릭 
     상세보기화면 ------------> 수정하기 화면 --------->  수정 처리 
     (view.jsp)               (edit.jsp)   작성완료 클릭(editController.java)
        |   /\                 파일다운로드                 |
        |   |            (DownloadController.java)         |
        |   |-----------------------------------------------
        |
        \/
    삭제 처리         
    (DeleteContoroller.java , delete.jsp)
```


### 4) 요청명

|기능|매핑방법|요청명|컨트롤러(서블릿)|뷰경로|
|---|--------|-----|---------------|------|
|목록보기|web.xml|/board/list.do|ListController|/board/list.jsp|
|글쓰기|web.xml|/board/write.do|Writecontroller|/board/write.jsp|
|상세보기| 애너테이션|/board/view.do|viewController|/board/view.jsp|
|비밀번호 검증|--|/board/pass.do|PassController|/board/pass.jsp|
|수정| 애너테이션|/board/edit.do|Editcontroller|/board/edit.jsp|
|삭제| 애너테이션|--|PassController|--|
|다운로드| 애너테이션|/board/downliad.do|DownloadController|--|

## 5. 페이징 쿼리문 (Paging)

* 게시판에서는 목록을 보통 10 ~ 20개 정도 나눠 페이지별로 출력함. 
    * 이러한 기법을 페이징 이라고 함
* 다음게시물 boardDao.java에 구현

### 1) rownum

* 가상의 컬럼
* select 쿼리문을 추출하는 데이터(ROW)에 순차적으로 부여되는 순번(NUM)을 말함.
* 컬럼은 만든적이 없지만 순번이 출력됨

### 2) 페이징 처리 위한 두가지 기본 설정값

* 한 페이지에 출력할 게시물 개수 : 10
* 한 화면(블럭)에 출력 할 페이지 번호의 개수 : 5

* web.xml (프로젝트 web.xml)

```xml
    ...
  <!-- 게시판 페이징 처리 위한 설정 값 -->
  <context-param>
  	<param-name>POSTS_PER_PAGE</param-name>
  	<param-value>10</param-value>
  </context-param>
  <context-param>
  	<param-name>PAGE_PER_BLOCK</param-name>
  	<param-value>5</param-value>
  </context-param>
</web-app>
```

### 3) 페이징 구현

* 저장된 전체 레코드 수 카운트 

#### 1. 각 페이지에서 출력할 게시물 범위 계산

##### 예

```java
현재 1 페이지 일때

    시작 값 : (1-1)*10 + 1 = 1
    종료 값 : (1*10) = 10

현재 2 페이지 일때

    시작 값 : (2-1)*10 + 1 = 11
    종료 값 : (2*10) = 20
```

##### 계산식

* 범위의 시작 값 : (현재 페이지 - 1) * POSTS_PER_PAGE + 1
* 범위의 종료 값 : (현재 페이지 * POSTS_PER_PAGE)

#### 2. 전체 페이지 수 계산

##### 예

```java
게시물 수가 총 105개
    
    페이지 수 : Math.ceil(105/10) = Math.ceil(10.5) -> 11
```

##### 계산식

```java
    Math.ceil(전체 게시물 수 / POSTS_PER_PAGE)
```

#### 3. 이전 페이지 블록 바로가기 출력

##### 예

```java
현재 1페이지 일때
    pageTemp = ((1-1)/5) * 5 + 1 = 1

현재 5페이지 일때
    pageTemp = ((5-1)/5) * 5 + 1 = 1 
    // pageTemp가 1이라 함은 첫번째 페이지 블록을 뜻함
    // 이전 페이지 블록 바로가기를 출력하지 않음

현재 6페이지 일때
    pageTemp = ((6-1)/5) * 5 + 1 = 6

현재 10페이지 일때
    pageTemp = ((10-1)/5) * 5 + 1 = 6
    // 1이 아닐때는 이전 페이지 블록 바로가기를 출력함
    // pageTemp - 1결과로 이전 페이지 블록 바로가기 출력함
```

##### 계산식

```java
    ((현재 페이지 - 1)/PAGES_PER_BLOCK) * PAGES_PER_BLOCK + 1
```

#### 4. 각 페이지 번호 출력

##### 예

```java
pageTemp가 1일때 : "1 2 3 4 5"를 출력
pageTemp가 6일때 : "6 7 8 9 10" 를 출력
```

## 6. controller 작성 - 글 목록

### 1) 서블릿 매핑 web.xml 등록

```xml
  <!-- 서블릿 매핑 -->
  <servlet>
  	<servlet-name>BoardList</servlet-name>
  	<servlet-class>kr.co.ezenac.model2.board.ListController</servlet-class>
  </servlet> 
  <servlet-mapping>
  	<servlet-name>BoardList</servlet-name>
  	<url-pattern>/board/list.do</url-pattern>
  </servlet-mapping>
  <servlet-name>BoardWrite</servlet-name>
  	<servlet-class>kr.co.ezenac.model2.board.WriteController</servlet-class>
  </servlet> 
  <servlet-mapping>
  	<servlet-name>BoardWrite</servlet-name>
  	<url-pattern>/board/write.do</url-pattern>
  </servlet-mapping> 
  
  <!-- 첨부 파일 최대 용량 설정 -->
   <context-param>
   		<param-name>maxPostSize</param-name>
   		<param-value>10240000</param-value>
   </context-param>
```

### 2) List Controller , jsp

![alt](/assets/images/post/jsp/142.png)

## 7. 글쓰기

![alt](/assets/images/post/jsp/141.png)

## 8. 상세보기 

![alt](/assets/images/post/jsp/150.png)

## 9. 다운로드

![alt](/assets/images/post/jsp/157.png)

## 10. 삭제하기

![alt](/assets/images/post/jsp/160.png)

## 11. 수정하기

![alt](/assets/images/post/jsp/163.png)

<a href="https://github.com/nicednjsdud/JSP/tree/main/workspace-jsp/chap15_BoardModel2">여기에 소스가 있습니다.</a>












































