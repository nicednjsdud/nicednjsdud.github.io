---
title: (Spring) 16. Spring Web Scope
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Spring Web Scope
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 웹 스코프 (Spring)

## 1. 웹 스코프에 특징

- 웹 스코프는 웹 환경에서만 동작한다.
- 웹 스코프는 프로토타입과 다르게 스프링이 해당 스코프의 종료시점까지 관리한다.
  - 따라서 종료 메서드가 호출된다.

## 2. 웹 스코프의 종류

### 1) request

- Http 요청 하나가 들어오고 나갈때 까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의 빈 인스턴스가  
  생성되고, 관리된다.

### 2) session

- HTTP Session과 동일한 생명주기를 가지는 스코프

### 3) application

- 서블릿 컨텍스트(**'ServletContext'**)와 동일한 생명주기를 가지는 스코프

### 4) websocket

- 웹 소켓과 동일한 생명주기를 가지는 스코프

## 2. Request Test

### 1) logger 찍어보기

```java
package kr.co.hellospring.web;

import kr.co.hellospring.common.MyLogger;
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.ObjectProvider;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;

@Controller
@RequiredArgsConstructor
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final ObjectProvider<MyLogger> myLoggerObjectProvider;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request){
        MyLogger myLogger = myLoggerObjectProvider.getObject();
        String requestURL = request.getRequestURL().toString();
        myLogger.setRequestURL(requestURL);

        myLogger.log("controller test");
        logDemoService.logic("testId");
        return "OK";
    }
}

```

- 로그를 출력하기 위한 `'MyLogger'` 클래스이다.
- `'@Scope(value="request")`를 사용해서 request 스코프로 지정했다.
- 이 빈은 HTTP 요청당 하나씩 생성되고, HTTP 요청이 끝나는 시점에 소멸된다.
- 이 빈이 생성되는 시점에 자동으로 `@PostConstruct` 초기화 메서드를 사용해서 uuid를 생성해서  
  저장해 둔다.
- `requestURL`은 이빈이 생성되는 시점에는 알 수 없으므로, 외부에서 setter로 입력 받는다.

### 2) LogDemoController

```java
package kr.co.hellospring.web;

import kr.co.hellospring.common.MyLogger;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;

@Controller
@RequiredArgsConstructor
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final MyLogger myLogger;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request){
        String requestURL = request.getRequestURL().toString();
        myLogger.setRequestURL(requestURL);

        myLogger.log("controller test");
        logDemoService.logic("testId");
        return "OK";
    }
}
```

- 로거가 잘 작동하는지 확인하는 테스트용 컨트롤러다.
- HttpServletRequest를 통해서 요청 URL을 받는다.

```
    requestURL 값 : http://localhost:8080/log-demo
```

- 컨트롤러에서 controller test라는 로그를 남긴다.

### 3. LogDemoService

```java
package kr.co.hellospring.web;

import kr.co.hellospring.common.MyLogger;
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.ObjectProvider;
import org.springframework.stereotype.Service;

@Service
@RequiredArgsConstructor
public class LogDemoService {

    private final ObjectProvider<MyLogger> myLoggerObjectProvider;

    public void logic(String id) {
        MyLogger myLogger = myLoggerObjectProvider.getObject();
        myLogger.log("service id = " + id);
    }
}
```

#### 4. result

- log

```java
[af2b18ff-a107-4196-a92b-693d6ae29e9c] request scope bean create:kr.co.hellospring.common.MyLogger@3510b558
[af2b18ff-a107-4196-a92b-693d6ae29e9c][http://localhost:8080/log-demo] controller test
[af2b18ff-a107-4196-a92b-693d6ae29e9c][http://localhost:8080/log-demo] service id = testId
[af2b18ff-a107-4196-a92b-693d6ae29e9c] request scope bean close:kr.co.hellospring.common.MyLogger@3510b558
```
