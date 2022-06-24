---
title: JSP 16. JSTL (2)
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
last_modified_at: '2022-06-11 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JSTL
======

## 8. ```<c:forEach>``` 태그

* JSP 페이지에서 반복문 수행하는 태그
* 일반 for문 형태

```html
<c:forEach var="변수명" 
           begin="시작값" 
           end="마지막값" 
           step="증가값" 
           varStatus="반복상태를 알려주는 변수이름" >
</c:forEach>
```

![alt](/assets/images/post/jsp/125.png)

* 향샹된 for문 형태

```html
<c:forEach var="변수명" items="반복할 객체이름" />
```

![alt](/assets/images/post/jsp/126.png)

### 1) varStatus의 속성을 통해 얻을 수 있는 정보

* current : var에 지정한 현재 루프의 변수값을 반환
* index : var에 지정한 현재 루프의 변수값 반환
* count : 실제 반복 횟수 
* first : 루프의 처음일때 true를 반환
* last : 루프의 마지막일때 true를 반환

##  9. ```<c:forTokens>``` 태그

* 구분자를 기준으로 문자열을 나눠 토큰의 개수만큼 반복해 줌
* 태그형식

```html
	<c:forTokens items="문자열" delims="문자열 구분자" var="변수명" />
```

```html
<title>JSTL - forTokens </title>
</head>
<body>
	<%String rgba = "Red,Green,Blue,Black";%>
	
	<h4>JSTL forTokens 태그</h4>
	
	<!--구분된 토큰 개수 만큼 반복함 -->
	<c:forTokens items="<%=rgba %>" delims="," var="color">
		<span style="color: ${color};">${color }</span><br/>
	</c:forTokens>
	<br/>
	
	<c:set var="fruits" value="사과,파인애플,바나나,망고,귤"/>
	
	<c:forTokens items="${fruits }" delims="," var="token">
		${token }<br/>
	</c:forTokens>
</body>
```

![alt](/assets/images/post/jsp/127.png)

## 10. ```<c:import>``` 태그

* <jsp:include> 액션태그와 같은 기능
* 외부 파일을 현재 위치에 삽입할 때 사용함
* 외부의 페이지도 삽입 할수 있음
* 태그형식 

```html
	<c:imprt url ="페이지 경로 혹은 URL" scope="영역" />
```

* import.jsp

```html
<body>
	<c:set var="requestVar" value="BOBdev" scope="request" />
	<c:import url="JStL02/inc/otherPage.jsp" var="contents">
		<!-- 포함될 페이지로 전달할 매개변수 추가 -->
		<c:param name="userParam1" value="JSP" />
		<c:param name="userParam2" value="Spring"/>
	</c:import>
	${contents }
</body>
```

* otherPage.jsp

```html
<ul>
	<li>저장된 값 : ${requestVar }</li>
	<li>매개변수 1 : ${param.userParam1 }</li>
	<li>매개변수 2 : ${param.userParam2 }</li>
</ul>
```

![alt](/assets/images/post/jsp/128.png)

## 11. ```<c:redirect>``` 태그
* 페이지 이동 처리
	* 매개 변수를 전달하고 싶다면 <c:param> 태그 사용하면 됨
* 태그형식

```html
	<c:redirect url="이동할 경로 및 URL" />
```

```html
<body>
	<c:set var="requestVar2" value="밥블로그" scope="request" />
	<!-- 리다이렉트는 포워드와 달리 request 영역은 공유되지 않음 -->
	<c:redirect url="/JSTL02/inc/otherPage.jsp">
		<c:param name="userParam1" value="BoB's Blog" />
		<c:param name="userParam2" value="밥쓰 블로그" />
	</c:redirect>
</body>
</html>
```

![alt](/assets/images/post/jsp/129.png)

## 12. ```<c:url>``` 태그
* 지정한 경로와 매개변수를 이용해서 url 생성함
* 생성된 url은 ```<a> 태그의 href속성, <form>태그의 action 속성```에 사용
* 태그형식

```html
	<c:url value="설정한 경로" scope="영역" var="변수명" />
```

* url.jsp

```html
	<title>JSTL - URL</title>
</head>
<body>
	<c:url value="/JSTL02/inc/otherPage.jsp" var="url">
		<c:param name="userParam1" value="BOB!" />
		<c:param name="userParam2">Hello JSTL!</c:param>
	</c:url>
	<a href="${ url}">otherPage.jsp 바로가기</a>
</body>
```

![alt](/assets/images/post/jsp/130.png)
![alt](/assets/images/post/jsp/131.png)

## 13. ```<c:out>``` 태그

* 변수 출력시 사용
* 출력할 변수가 null일때 default 속성에 지정한 기본값 출력이 됨.
* escapeXml 속성을 true로 설정하면 특수기호를 그대로 출력함
* 태그형식

```html
<c:out value="출력할 변수" default="기본값" escapeXml="특수문자 변환여부" />
```

* out.jsp

```html
<body>
	<c:set var="iTag" > i 태그는 <i>기울임</i>을 표현합니다.</c:set>
	<c:out value="${iTag }" />
	
	<h4>escapeXml 속성</h4>
	<c:out value="${iTag }" escapeXml="false"/>
	
	<h4>default 속성</h4>
	<!-- 변수값이 null인 경우이므로 default 속성값이 출력됨 -->
	<c:out value="${param.name }" default="empty" />
	
	<h4>빈 문자열일때<h4>
	<!-- 빈 문자열도 하나의 값이므로(null이 아님) 
			default 속정에 지정한 값이 출력되지 않음 -->
	<c:out value="" default="출력이 안되네요" />
</body>
```

![alt](/assets/images/post/jsp/132.png)

## 14. ```<c:catch>``` 태그

* 발생한 예외를 잡아 처리하는 역할
* 지정한 변수에 에러 메시지가 저장되어 전달됨
* 태그형식

```html
	<c:catch var="변수명">
		실행코드
	</c:catch>
```

* catch.jsp

```html
<body>
	<% int num1 = 100; %>
	<!-- catch 태그 블록 안의 스클릿틀릿에서 예외 일어남
		=> 이 발생한 예외를 catch 태그가 잡아 eMessage에 저장
	 -->
	<c:catch var="eMessage">
		<% int result = num1/0;%>
	</c:catch>
	예외 내용 : ${eMessage }
</body>
```

![alt](/assets/images/post/jsp/133.png)
