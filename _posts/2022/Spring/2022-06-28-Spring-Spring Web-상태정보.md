---
title: (Web) 웹에서의 상태 유지 기술 (Cookie & Session)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Cookie & Session
tag: Spring Web
article_tag1: Spring Basic
article_section: Spring Basic
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-06-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 웹에서의 상태 유지 기술 (Cookie & Session)

## 1. 웹에서의 상태 유지 기술

### 1) HTTP프로토콜은 상태 유지가 되지 않은 프로토콜이다.

- 이전에 무엇을 했고, 지금 무었을 했는지에 대한 정보를 갖고 있지않음.
- 웹 브라우저의 요청에 대한 응답을 하고 나면 해당 클라이언트와의 연결을  
  지속하지않음.

### 2) 상태 유지를 위해 Cookie와 Session 기술이 등장함.

## 2. 쿠키(Cookie)와 세션(Session)

### 1) 쿠키

- 사용자 컴퓨터에 저장
- 저장된 정보를 다른 사람 또는 시스템이 볼 수 있는 단점
- 유효기간이 지나면 사라짐

### 2) 세션

- 서버에 저장
- 서버가 종료되거나 유효시간이 지나면 사라짐

### 3) 쿠키 동작 이해

```js
                request(1)
                --------->
    웹 클라이언트               WAS (2)쿠키생성
                <---------
                response(3)
```

```js
                request(4 쿠키 포함)
                --------->
    웹 클라이언트               WAS (5)쿠키를 받아 검사
                <---------

```

### 4) 세션 동작 이해

```js
                request(1)
                --------->
    웹 클라이언트               WAS (2) 세션키 생성
                <---------         (3) 세션키를 이용한 저장소 생성
                response(5)        (4) 세션키를 담은 Cookie 생성
                세션키를 담은쿠키
                포함
```

```js
                request(6 세션키를 저장하고 있는 쿠키)
                --------->
    웹 클라이언트               WAS (7)쿠키의 세션키를 이용해 이전에 생성한
                <---------            저장소를 활용

```

## 3. 쿠키 정의

### 1) 정의

- 클라이언트 단에 저장되는 작은 정보의 단위
- 클라이언트에서 생성하고 저장될 수 있고, 서버단에서 전송한 쿠키가 클라이언트  
  에 저장될 수있다.

### 2) 이용 방법

- 서버에서 클라이언트의 브라우저로 전송되어 사용자의 컴퓨터에 저장
- 저장된 쿠키는 다시 해당하는 웹페이지에 접속할 때, 브라우저에서 서버로  
  쿠키를 전송
- 쿠키는 이름(name)과 값(value)으로 구성된 자료를 저장

### 3) 쿠키는 그 수와 크기에 제한

- 하나의 쿠키는 4K Byte 크기로 제한
- 브라우저는 각각의 웹사이트 당 20개의 쿠키를 허용
- 모든 웹 사이트를 합쳐 최대 300개를 허용
- 그러므로 클라이언트 당 쿠키의 최대 용량은 1.2M Byte

### 4) 쿠키의 유효시간 설정

#### 1. 메소드 setMaxAge()

- 인자는 유효기간을 나타내는 초단위의 정수형
- 만일 유효기간을 0으로 지정하면 쿠키의 삭제
- 음수를 지정하면 브라우저가 종료될 때 쿠키가 삭제

#### 2. 유효기간을 10분으로 지정하려면

```js
cookie.setMaxAge(10 * 60); // 초 단위 : 10분
```

- 1주일로 지정하려면 (7*24*60\*60)로 설정한다.

### 5) Spring MVC에서의 Cookie 사용

#### @CookieValue 애노테이션 사용

- 컨트롤러 메소드의 파라미터에서 CookieValue애노테이션을 사용함으로써 원하는  
  쿠키정보를 파라미터 변수에 담아 사용할 수 있다.

```java
컨트롤러메서드(@CookieValue(value="쿠키이름",required=false,
                    defaultValue="기본값")String 변수명)
```

- GuestbookController.java

```java
@GetMapping(path="/list")
	public String list(@RequestParam(name="start",required=false,defaultValue="0")
			int start,ModelMap model, @CookieValue(value="count", defaultValue="0",required=true)String value,
						HttpServletResponse response) {



		try {
				int i=Integer.parseInt(value);
				value= Integer.toString(++i);
		}catch(Exception e) {
				value="1";
		}


		Cookie cookie = new Cookie("count",value);	// 쿠키생성
		cookie.setMaxAge(60*60*24*365);
		cookie.setPath("/");
		response.addCookie(cookie);
        ...
}
```

## 4. 세션 정의

### 1) 정의

- 클라이언트 별로 서버에 저장되는 정보

### 2) 이용방법

- 웹 클라이언트가 서버측에 요청을 보내게 되면 서버는 클라이언트를 식별하는  
  session id를 생성
- 서버는 session id를 이용해서 key와 value를 이용한 저장소인 HttpSession 생성
- 서버는 session id를 저장하고 있는 쿠키를 생성하여 클라이언트에 전송
- 클라이언트는 서버측에 요청을 보낼때 session id를 가지고 있는 쿠키를 전송
- 서버는 쿠키에 있는 session id를 이용해서 그 전 요청에서 생성한  
  HttpSession을 찾고 사용한다.

### 3) 세션에 값 저장

```java
    setAttribute(String name,Object value)
```

- name과 value의 쌍으로 객체 Object를 저장하는 메소드
- 세션이 유지되는 동안 저장할 자료를 저장

### 4) 세션에 값 조회

```java
    getAtrribute(String name)
```

- 반환 값은 Object 유형이므로 저장된 객체로 자료유형 변환이 필요
- 메소드 setAttribute()에 이용한 name인 "id"를 알고 있다면 바로 다음처럼 조회

```java
    String value=(String) session.getAttribute("id");
```

### 5) 세션에 값 삭제

```java
    removeAttribute(String name)
```

- name값에 해당하는 세션 정보를 삭제한다.

```java
    invalidate()
```

- 모든 세션 정보를 삭제한다.

### 6) javax.servlet.http.HttpSession

![alt](https://cphinf.pstatic.net/mooc/20180221_274/15191943441196AM5W_PNG/1.png?type=w760)

![alt](https://cphinf.pstatic.net/mooc/20180221_271/1519194381710ssK9b_PNG/2.png?type=w760)

#### 세션은 클라이언트가 서버에 접속하는 순간 생성

- 특별히 지정하지 않으면 세션의 유지 시간은 기본 값으로 30분 설정
- 세션의 유지 시간이란 서버에 접속한 후 서버에 요청을 하지 않은 최대 시간
- 30분 이상 서버에 전혀 반응을 보이지 않으면 세션이 자동으로 끊어짐
- 이 세션 유지 시간은 web.xml 파일에서 설정 가능

```xml
    <session-config>
     <session-timeout>30</session-timeout>
    </session-config>
```

출처 :<a href="https://www.boostcourse.org/web326/lecture/58991?isDesc=false">boostcourse 1) 상태정보란?</a>
