---
title: JSP 13. 액션태그
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
last_modified_at: '2022-06-06 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

액션 태그
=========

## 액션 태그(Action Tag)

* JSP 표준 태그
* 페이지 사이에서 이동을 제어하거나 자바빈을 생성할 때 주로 사용함.
* 특별한 선언없이 <jsp: 태그명 /> 형태로 사용함.
* 태그처럼 사용하지만 그 뒤에서는 JSP가 수행됨. 
    * WAS에서 처리된 후 결과만 출력함.

## 액션 태그 특징

* XML 문법 따름
* 반드시 종료 태그를 사용해야 함.
* 액션 태그 사이에 주석을 사용하면 에러가 발생함.
* 액션 태그에 속성값을 부여할 때는 표현식(<%= %>)을 사용할 수 있음.

## 용도에 따른 구분

```jsp
    <jsp:include></jsp:include>
    <jsp:forward></jsp:forward>
    <jsp:useBean></jsp:useBean>,<jsp:setProperty></jsp:setProperty>,
                                <jsp:getProperty></jsp:getProperty>
    <jsp:param></jsp:param>
```

## <jsp:include>

* 외부 JSP 파일을 현재 JSP 파일로 포함시키는 기능

|   | include 지시어 |  < jsp:include > 액션 태그|
|---|---------------|-------------------------|
|형식|<%@ include file="포함할 파일의 경로"%> | < jsp:include page="포함할 파일의 경로명" >|
|포함방식| 페이지 자체를 현재 페이지에 포함시킨 후 컴파일 진행| 실행의 흐름을 포함시킬 페이지로 이동시킨 후 실행한 결과를 현재 페이지에 포함시킴.|
|변수| 포함시킨 파일에서 생성한 변수를 사용 가능 | 포함시킨 파일에서 생성한 변수 사용 불가 |
|page 영역| 공유됨 | 공유되지 않음|
|request 영역| 공유됨 | 공유됨 |

* outerPage1.jsp

```jsp
	<h2>외부 파일1</h2>
	<% String newVar1 = "BOB's Blog"; %>
	<ul>
		<li>page 영역 속성 : <%= pageContext.getAttribute("pAttr") %></li>
		<li>request 영역 속성 : <%= request.getAttribute("rAttr") %></li>
	</ul>
```

* outerPage2.jsp

```jsp
	<h2>외부 파일2</h2>
	<% String newVar2 = "BOB's Programming"; %>
	<ul>
		<li>page 영역 속성 : <%= pageContext.getAttribute("pAttr") %></li>
		<li>request 영역 속성 : <%= request.getAttribute("rAttr") %></li>
	</ul>
```

* includeMain.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	// 포함할 두 파일의 경로를 변수에 저장
	String outerPage1 = "./inc/outerPage1.jsp";
	String outerPage2 = "./inc/outerPage2.jsp";
	
	// Page영역과 request영역에 속성 저장
	pageContext.setAttribute("pAttr", "세종대왕");
	request.setAttribute("rAttr", "이순신");
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>지시어와 액션태그 동작 방식 비교</title>
</head>
<body>
	<h2>지시어와 액션태그 동작 방식 비교</h2>
	
	<!-- 지시어 방식  -->
	<%@ include file="./inc/outerPage1.jsp" %>
	<p>외부 파일1 에 선언한 변수 : <%=newVar1 %></p>
	
	<!-- 액션 태그 -->
	<h3>액션 태그로 페이지 포함하기</h3>
	<jsp:include page="./inc/outerPage2.jsp" />
	<jsp:include page="<%= outerPage2 %>" />
	<p>외부 파일2 에 선언한 변수 : <%-- <%=newVar2 %> --%></p>	
						<!-- 존재하지 않으니 출력되지 않음 Err -->
</body>
</html>
```

![alt](/assets/images/post/jsp/85.png)

## <jsp:forward>

![alt](/assets/images/post/jsp/88.png)

* 포워드는 현재 페이지에 들어온 요청을 다음 페이지로 보내는 기능
* 포워드는 버퍼를 사용함
* 다음 페이지로 요청을 전달 하는 것이 목적
	* 이동된 페이지와 request 영역을 공유함
	* URL이 변경되지 않는 특징이 있음.

* fowardMain.jsp

```jsp
	<%@ page language="java" contentType="text/html; charset=UTF-8"
		pageEncoding="UTF-8"%>
	<%
		pageContext.setAttribute("pAttr", "이방원");
		request.setAttribute("rAttr", "이도");
	%>
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>액션 테그 - forward</title>
	</head>
	<body>
		<h2>액션 태그를 이용한 포워딩</h2>
		<jsp:forward page="forwardSub.jsp" />
	</body>
	</html>
```

* fowardSub.jsp

```jsp
	<title>액션태그 - forward</title>
	</head>
	<body>
		<h2>포워드 결과</h2>
		<ul>
			<li>
				page영역 : <%=pageContext.getAttribute("pAttr") %>
			</li>
			<li>
				request영역 : <%=request.getAttribute("rAttr") %>
			</li>
		</ul>

```
![alt](/assets/images/post/jsp/87.png)

## <jsp:useBean>, <jsp:setProperty>, <jsp:getProperty>

* 자바빈즈(JavaBeans)를 생성하거나 설정 할 때 사용
* 자바빈즈는 데이터를 저장하기 위한 멤버 변수, 게터/세터 메서드로만 이루어진 클래스.
	* 기본(default) 패키지 이외의 패키지에 속해 있어야 함.
	* 멤버 변수(속성, 프로퍼티)의 접근 지정자는 private으로 선언함
	* 기본 생성자가 잇어야 함.
	* 멤버 변수에 접근할 수 있는 게터/세터 메서드 있어야 함.
	* 게터/세터 메서드의 접근 지정자는 pubilc 이어야 함.

### 1) 자바빈즈 생성

```jsp
 <jsp:useBean id="자바빈즈 이름" class="사용할 패키지와 클래스명" scope="저장 될 영역" />
```

* id : 자바빈즈 객체의 이름 지정
* class : 사용하려는 자바빈즈 객체의 실제 패키지명과 클래스명 지정
* scope : 자바진즈가 저장될 내장 객체 영역 지정
	* 생략한다면 기본값인 page 영역이 지정

#### 자바빈즈 생성할 때는 기본 생성자 호출
* 기본생성자가 없다면 에러가 남

### 2) 멤버 변수 값 설정/추출

```jsp
	<jsp:setProperty name="자바빈즈 이름" property="속성명(멤버 변수)" value="설정할 값" />
```

* name : userBean의 id속성에 지정한 자비빈즈 이름을 지정
	* 인스턴스 변수를 지정하는 것과 동일
* property : 자바빈즈의 멤버 변수명 
* value : 멤버 변수에 설정할 값 지정

```jsp
	<jsp:getProperty name="자바빈즈 이름" property="속성명(멤버 변수)" />
```

* UseBeanMain.jsp

```jsp
	<%@page import="kr.co.ezenac.bean.Person"%>
	<%@ page language="java" contentType="text/html; charset=UTF-8"
		pageEncoding="UTF-8"%>
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>액션 태그 - UseBean</title>
	</head>
	<body>
		<h2>UseBean 액션 태그</h2>
		<h3>자바빈즈 생성하기</h3>
		<jsp:useBean id="person" class="kr.co.ezenac.bean.Person" scope="request" />
		
		
		<!-- 액션 태그로 자바빈즈를 생성할 때는 기본 생성자를 사용하고,
			값을 설정할때는 세터 , 값을 추출할때는 게터 메서드를 사용함. -->
		<h3>액션태그로 자바빈즈 속성 지정하기</h3>
		<jsp:setProperty property="name" name="person" value="정도전" />
		<jsp:setProperty property="age" name="person" value="40" />
		
		<h3>액션테그로 자바빈즈 속성 지정하기</h3>
		<ul>
			<li>이름 : <jsp:getProperty property="name" name="person"/></li>
			<li>나이 : <jsp:getProperty property="age" name="person"/></li>
		</ul>
	</body>
	</html>
```

![alt](/assets/images/post/jsp/89.png)

### 3) 와일드카드 (*)로 폼값 한번에 설정

* property 속성에 와일드카드를 사용하면 <form> 태그를 통해 전송되는 모든 폼값을 한번에 자바빈즈에 입력할 수 있음.
  

* UseBeanForm.jsp

```jsp
	<body>
		<h2>액션 태그로 폼값 한 번에 받기</h2>
		<form method="post" action="useBeanAction.jsp">
			이름 : <input type="text" name="name" /><br>
			나이 : <input type="text" name="age" />
			<input type="submit" value="폼값 전송" />
		</form>
	</body>
```

* UseBeanAction.jsp

```jsp
<body>
	<h3>액션 태그로 폼값 한 번에 받기</h3>
	<jsp:useBean id="person" class="kr.co.ezenac.bean.Person" />
	<jsp:setProperty property="*" name="person"/>
	
	<ul>
		<li>이름 : <jsp:getProperty property="name" name="person"/> </li>
		<li>나이 : <jsp:getProperty property="age" name="person"/> </li>
	</ul>
</body>
```

![alt](/assets/images/post/jsp/90.png)

## <jsp:param>

![alt](/assets/images/post/jsp/91.png)

* paramMain.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	request.setCharacterEncoding("utf-8");
	String pValue = "대한민국";
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>액션 태그 - param</title>
</head>
<body>
	<jsp:useBean id="oerson" class="kr.co.ezenac.bean.Person" scope="request" />
	<jsp:setProperty property="name" name="person" value="이순신"/>
	<jsp:setProperty property="age" name="person" value="42"/>
	<jsp:forward page="paramForward.jsp?param1=류현진">
		<jsp:param value="경기도 용인시" name="param2"/>
		<jsp:param value="<%=pValue %>" name="param3"/>
	</jsp:forward>
</body>
</html>
```

* paramForward.jsp

```jsp
<body>
	<jsp:useBean id="person" class="kr.co.ezenac.bean.Person" scope="request" />
	<h2>포워드된 페이지에서 매개변수 확인</h2>
	<ul>
		<li><jsp:getProperty property="name" name="person"/> </li>
		<li>나이 : <%= request.getParameter("param1") %> </li>
		<li>나이 : <%= request.getParameter("param2") %> </li>
		<li>나이 : <%= request.getParameter("param3") %> </li>
	</ul>
</body>
```

![alt](/assets/images/post/jsp/92.png)

## jsp:param

* 다른 페이지로 매개변수를 전달함.
* jsp:include, jsp:forward 액션 태그와 함께 사용
* 페이지 사이의 매개변수는 모두 request 영역에 생성됨.

* paramFoward.jsp

```jsp
	<!-- include한 jsp페이지와는 변수를 직접 공유 불가 -->
	<jsp:include page="inc/paramInclude.jsp"  >
		<jsp:param value="경기도 양평군" name="Loc1"/>
		<jsp:param value="용문면" name="Loc2"/>
	</jsp:include>
	<!-- jsp:param include한 페이지로도 매개변수 전달 가능 -->
```

* inc/paramInclude.jsp

```jsp
	<%@ page language="java" contentType="text/html; charset=UTF-8"
		pageEncoding="UTF-8"%>
	<h2>인클루드된 페이지에서 매개변수 확인</h2>
	<%=request.getParameter("Loc1") %>에
	<%=request.getParameter("Loc2") %>이있습니다.
```

![alt](/assets/images/post/jsp/93.png)