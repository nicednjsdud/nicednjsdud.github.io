---
title: JSP 10. 쿠키
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
last_modified_at: '2022-05-28 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

쿠키
====

## 쿠키(Cookie)란?

### 클라이언트의 상태 정보를 유지하기 위한 기술임.

#### 1) 웹사이트가 방문자를 기억하는 수단
* 언제 방문했는지, 어떤 페이지를 클릭했는지, 어떤 상품을 구매했는지 등 기록해  
  두었다가 이를 활용하여 맞춤 서비스, 로그 분석, 속도 개선 등 할수 있음.
* 웹페이지들 사이의 고유 정보를 클라이언트 PC에 저장해 놓고 사용하는 방법

#### 2)

* 상태 정보를 클라이언트 주로 웹 브라우저에 키(key)와 값(value) 형태로 저장했다가   
  다음 요청시 저장된 쿠키를 함께 전송함 

    => 웹 서버는 브라우저가 전송한 쿠키로부터 필요한 데이터를 읽어올 수 있음.
        
- 3000개까지 만들수 있음.
- 쿠키 하나의 최대 크기는 4096바이트임.
- 보안이 취약함
     - 클라이언트 브라우저에서 사용 유무를 설정가능
- 하나의 호스트나 도메인에서 최대 50개까지 만들 수 있음. 

## 레이어 팝업

* 웹 애플리케이션 개발할 때 팝업창을 많이 사용하게 됨
* 회원 가입 시 아이디 중복체크, 간단한 공지사항 띄워주는 용도
* "하루동안 열지 않음"과 같은 문구가 쓰여진 팝업창 형태

### 1) 동작 예시 

* 메인 화면

```
    - 팝업 공지                 닫기 => 사라짐
    ("하루동안 열지 않음") 
```

* cookieMain.jsp

```js
<script
	src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script type="text/javascript">
$(function popBtn() {
	$('#closeBtn').click(function() { /* 닫기 버튼을 누르면 */

		$('#popup').hide() /* 팝업창을 숨김 처리함 */

		/* [오늘 하루 열지 않음]을 체크했는지를 확인하여  쿠키를 설정
		 --popupCookie.jsp 실행*/
		/* id가 inactiveToday이면서 "체크된" 체크박스 */	

		/* 값을 읽어옴 => chkVal에 1저장됨 */
		let chkVal = $('input:checkbox[id="inactiveToday"]').val()

		/* jQuery의 ajax() : 비동기 HTTP 요청을 보내는 함수 */
		$.ajax({		/* 4) 비동기 요청 보냄 */

		url : './popupCookie.jsp', /* 1) 요청을 보낼 페이지의 URL */

		type : 'get',/* 2) 'get', 'post' 등 http 메서드 지정 */

		data : {inactiveToday : chkVal}, /* 3) 서버로 보낼 데이터 */

		dataType : "text", 		
        /* 5) 서버로 부터 받은 응답 데이터의 타입은 일반 텍스트임 */

		success : function(resData){ /* 6) 요청 성공 시 실행할 콜백 함수 */
			if (resData !=''){
				location.reload() /* 7) 응답 데이터가 있다면  */
				}	
			}		/* 8) 페이지 새로고침 */
		})
	})
	})
</script>

```

![alt](/assets/images/post/jsp/70.png)

### 2) 쿠키를 이용해 상태정보 유지하기

* popupcookie.jsp

```js
<%
/* inactiveToday 매개변수 값 얻기 (체크박스 폼값)
	[오늘 하루 열지 않음] 체크박스를 체크했다면 이 값으로 "1"이 전될됨*/
String chkVal = request.getParameter("inactiveToday");
	
if(chkVal != null && chkVal.equals("1")){	
			/* 값이 1이면 쿠키를 생성해 응답 객체에 추가 */

	/* 이름이 "PopupClose", 값이 "off" 쿠키 생성 */
	Cookie cookie = new Cookie("PopupClose","off");	

	cookie.setPath(request.getContextPath());/* 경로 컨텍스트 루트 설정 */

		cookie.setMaxAge(60*60*24);		/* 유지 기간 하루인 쿠키 설정*/

		response.addCookie(cookie);		/* 응답 객체에 추가 */

		out.print("쿠키 : 하루 동안 열지 않음"); 
		/* 출력문자열은 success : function(resData)로 콜백됨 */
	}
%>

```

![alt](/assets/images/post/jsp/71.png)

## 로그인 아이디 저장

* 로그인에 성공한 경우에만 쿠키를 생성 및 삭제함.
* 쿠키에 저장된 아이디가 있다면 로그인 페이지에서는 아이디가 자동 입력됨
* [아이디 저장하기] 체크박스를 해제하고 로그인에 성공하면 쿠키가 삭제됨.

### 1) 동작 예시

#### 로그인 화면

* 체크 했을 떄

```
    아이디 [v] 아이디 저장하기 => 메인 화면 =(재방문) => 아이디(자동입력)
    비밀번호                                          비밀번호
    로그인(버튼)                                      로그인(버튼)        
```

* 체크 해제 했을 때

```
    아이디 [] 아이디 저장하기 => 메인 화면 =(재방문) => 아이디(저장된 아이디
                                                               삭제)
    비밀번호                                          비밀번호
    로그인(버튼)                                      로그인(버튼) 
    
```

### 2) 구현

##### 1.JS함수

```java
public class JsFunction {
	// 메세지 알림창을 띄우고 명시한 URL로 이동함.(ex. 로그인에 성공했습니다.
	public static void alertLocation(String msg, String url, JspWriter out) {
		try {
			String script = ""
							+"<script>"
							+"		alert( '"+msg+"')"
							+"		location.href='"+url+"' "
							+"</script>";
			out.print(script);
		}catch(Exception e) {
			
		}
	}
	
	// 메세지 알림창을 띄운후 이전 페이지로 돌아감 (ex.로그인에 실패했습니다.)
	public static void alertBack(String msg, JspWriter out) {
		try {
			String script = ""
							+"<script>"
							+"		alert( '"+msg+"')"
							+"		history.back()"
							+"</script>";
			out.print(script);
		}catch(Exception e) {
			
		}
	}
}

```

##### 2.cookieManger.java

```java
public class CookieManager {
	
	// 명시한 이름, 값, 유지기간 조건으로  
	public static void makeCookie(HttpServletResponse response, 
				String cName, String cValue,int cTime) {
		Cookie cookie = new Cookie(cName,cValue);	// 쿠키생성
		cookie.setPath("/");		
		// 경로 설정 - 웹 애플리케이션 전체에서 사용하는 쿠키 만듦
		cookie.setMaxAge(cTime);	// 유지 기간 설정
		response.addCookie(cookie); // 응답 헤더에 추가 => 클라이언트 쿠키를 전송함.
		
		
	}
	// 명시한 이름의 쿠키를 찾아, 그 값을 반환함
	public static String readCookie(HttpServletRequest request,String cName) {
		String cookieValue = "";
		
		// 클라이언트가 보내온 쿠키 목록을 받음
		Cookie[] cookies = request.getCookies();
		if(cookies !=null) {
			for(Cookie c: cookies) {
				String cookieName = c.getName();
				if(cookieName.equals(cName)) {
					cookieValue = c.getValue();
				}
			}
		}
		
		
		return cookieValue;
	}
	// 명시한 이름의 쿠키 삭제
	public static void deleteCookie(HttpServletResponse response, String cName) {
		
		// 쿠키 생성시 값은 빈 문자열로, 유지기간은 0으로 부여 
		makeCookie(response,cName,"",0);
	}
}
```

##### 3.로그인 페이지 작성

```jsp
<%
	// 이름이 loginId인 쿠키를 읽어와 loginId 변수에 저장함.
	String loginId = CookieManager.readCookie(request,"loginId" );

	String cookieCheck = "";
	if (!loginId.equals("")){
	// 쿠키에 저장된 아이디가 있다면 "loginID"에 빈 문자열 외의 문자열을 저장
		cookieCheck = "checked";
	}
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Cookie - 아이디 저장하기</title>
</head>
<body>
	<h2>로그인 페이지</h2>
	<form action="idSaveProcess.jsp" method="post">
		아이디 : <input type="text" name="user_id" value="<%=loginId %>" />
		<input type="checkbox" name="save_check" value="Y"<%=cookieCheck %> />
		<br />
		패스워드 : <input type="password" name="user_pw" />
		<br/>
		<input type="submit" value="로그인하기" />
	</form>
</body>
</html>
```


##### 4.로그인 및 아이디 저장 기능

```jsp
<%@page import="kr.co.ezenac.utils.CookieManager"%>
<%@page import="kr.co.ezenac.utils.JsFunction"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	String userId = request.getParameter("user_id");
	String userPw = request.getParameter("user_pw");
	String saveCheck = request.getParameter("save_check");
	
	if ("ezen".equals(userId) && "0824".equals(userPw)){
		// 로그인 성공
		if (saveCheck !=null && saveCheck.equals("Y")){	// [아이디 저장하기]체크 확인
			// 쿠키 생성
			CookieManager.makeCookie(response, "loginId", userId, 86400);
		}
		else {
			// 쿠키 삭제
			CookieManager.deleteCookie(response, "loginId");
		}
		JsFunction.alertLocation("로그인에 성공하였습니다.","idSaveMain.jsp", out);
	}
	else{
		// 로그인 실패
		JsFunction.alertBack("로그인에 실패했습니다.", out);
	}
%>
```

![alt](/assets/images/post/jsp/72.png)
![alt](/assets/images/post/jsp/73.png)
![alt](/assets/images/post/jsp/74.png)

## 서블릿으로 구현

### SetCookieValue.java

```java
@WebServlet("/set")
public class SetCookieValue extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		Date d = new Date();
		
		// Cookie 객체를 생성한 후 cookieTest 이름으로 한글정보를 인코딩해서 쿠키에 저장함
		Cookie c =  new Cookie("cookieTest", 
				URLEncoder.encode("Servlet 쿠키 프로그래밍입니다.","utf-8"));
		c.setMaxAge(24*60*60);		// 유효기간 설정(하루)
		response.addCookie(c);		// 생성된 쿠키를 브라우저로 전송함
		
		out.print("현재 시간 : "+d);
		out.print("현재 시간을 Cookie로 저장합니다.");
	}
}
```
![alt](/assets/images/post/jsp/75.png)

### getCookieValue.java

```java
@WebServlet("/get")
public class GetCookieValue extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		// 브라우저에게 쿠키 정보를 요청한 후 쿠키 정보를 배열로 가져옴
		Cookie[] allValues =request.getCookies();
		
// 배열에서 저장할 떄 사용한 쿠키 이름인 cookieTest로 검색해 쿠키 값을 가져옴
		for(Cookie value :allValues) {
			if(value.getName().equals("cookieTest")) {
				out.print(
				"<h2>cookie 값 가져오기 : "+URLDecoder.decode(value.getValue(),"utf-8")+
				"<h2>"
						);
				
			}
		}
	}
}    
```

![alt](/assets/images/post/jsp/76.png)
