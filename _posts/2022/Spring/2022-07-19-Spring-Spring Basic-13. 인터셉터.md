---
title: (Spring) 13. 인터셉터(Intercepter) 구현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: 인터셉터(Intercepter)
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-19 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Intercepter 구현

## 1. HandlerInterceptor 클래스

### 1) preHandle()

- 컨트롤러 실행 전 호출 됨

### 2) postHandle()

- 컨트롤러 실행 후 DispatcherServlet이 뷰로 보내기 전에 호출 됨

### afterCompletion()

- 뷰까지 수행하고 나서 호출 됨

## 2. JSP에서 다국어 표시

### 1) `<spring:message />`태그 이용함

- 형식

```java
	<spring:message code="properties의 키" text="기본값" />
```

## Interseptor TEST

- 컨트롤러로 요청을 받기전 요청명에서 파일을 잘라줄 인터셉터 생성

```java
package kr.co.tiles.member.interceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.handler.HandlerInterceptorAdapter;

// 사용자정의 인터셉터는 반드시 HandleriterceptorAdapter를 상속받아야 함
public class ViewNameInterceptor extends HandlerInterceptorAdapter {

	// 컨트롤러 실행 전 호출 함
	@Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
			throws Exception {
		String viewName = getViewName(request);
		request.setAttribute("viewName", viewName);//컨트롤러에게 request를 보냄

		return true;
	}
	private String getViewName(HttpServletRequest request) {

		String contextPath = request.getContextPath();	// member/*.do
		int begin = 0;
		if (!((contextPath == null) || ("".equals(contextPath)))) {
			begin = contextPath.length();		// 전체 요명의 길이

		}
		int end;

		// 주소창의 현재 uri받아오기
		String uri = (String) request.getAttribute("javax.servlet.include.request_uri");
		if (uri == null || uri.trim().equals("")) {
			uri = request.getRequestURI();
		}


		if (uri.indexOf(";") != -1) {
			end = uri.indexOf(";");
		} else if (uri.indexOf("?") != -1) {
			end = uri.indexOf("?");
		} else {
			end = uri.length();
		}
		String filename = uri.substring(begin, end);//	 /member/listMembers.do

		if (filename.indexOf(".") != -1) {
			filename = filename.substring(0, filename.lastIndexOf("."));	// 	/member/listMembers
		}

		if (filename.indexOf("/") != -1) {
	// /member/listMembers.do 요청 할 경우 member/listMembers를 파일이름으로 가져옴
			filename = filename.substring(filename.lastIndexOf("/",1), filename.length());	//   member/listMembers
		}
		return filename;
	}
}

```

### 2) MemberControllerImpl.java 클래스에 내용 추가

```java
	@Override
	@RequestMapping(value = "/member/listMembers.do", method = RequestMethod.GET)
	public ModelAndView listMembers(HttpServletRequest request, HttpServletResponse response) throws Exception {
		// 인터셉터에게 viewName을 받아옴
		String viewName = (String) request.getAttribute("viewName");

		ModelAndView mav = new ModelAndView(viewName);

		List<MemberDTO> membersList = memberService.listMembers();

		// 조회한 회원 정보를 ModelAndView의 addObject() 이용해 바인딩함.
		mav.addObject("membersList", membersList);

		return mav;
	}
```

### 3) 결과 창

- 컨트롤러에 요청사항대로 listMembers.do 에서 listMembers만 잘라옴

![alt](/assets/images/post/spring/34.png)
