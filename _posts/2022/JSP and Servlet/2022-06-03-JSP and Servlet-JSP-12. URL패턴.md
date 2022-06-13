---
title: JSP 12. URL 패턴
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
last_modified_at: '2022-06-03 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

URL 패턴
==========

## URL 패턴

* 서블릿 매핑 시 사용되는 가상의 이름
* 클라이언트가 브라우저에서 요청할 때 사용되며 반드시 /(슬래시)로 시작해야 함

### 1) exact mapping ( 이름까지 일치 )

```
                                ( 매칭 URL)
   /login/login.do  =>    http://localhost/chap09/login/login.do 
```

* UrlTest.java

```java
// 정확히 이름까지 일치하는 패턴
@WebServlet("/order/ezen")
public class UrlTest extends HttpServlet {
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
                                                    throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		// 컨텍스트 이름만 가져옴
		String context = request.getContextPath();
		System.out.println("컨텍스트 이름: "+context);
		// 전체 URL 가져옴
		String url = request.getRequestURL().toString();
		System.out.println("전체 URL : "+context);
		// 서블릿 매핑 이름만 가져옴
		String mapping = request.getServletPath();
		System.out.println("서블릿 매핑 이름 : "+mapping);
		// URI 가져옴
		String uri = request.getRequestURI();
		System.out.println("URI : "+uri);
		
		out.print("<html><body bgcolor='yellow'>");
		out.print("<b>UrlTest입니다.</b>");
		out.print("</html></body>");
	}
}
```

![alt](/assets/images/post/jsp/81.png)

### 2) path mapping (디렉터리까지 일치)

```
    /login/*        =>    http://localhost/login/
                          http://localhost/login/login
                          http://localhost/login/login.do
                          http://localhost/login/order/
```

```java
    // 디렉터리 이름까지 일치하는 패턴
    @WebServlet("/order/*")
```

![alt](/assets/images/post/jsp/82.png)


### 3) extension mapping (확장자만 일치)

```
    *.do            =>    http://localhost/chap09/login.do
                          http://localhost/chap09/order.do
                          http://localhost/chap09/login/logout.do
```

```java
    // 확장자만 일치하는 패턴
    @WebServlet("*.do")
```

![alt](/assets/images/post/jsp/83.png)