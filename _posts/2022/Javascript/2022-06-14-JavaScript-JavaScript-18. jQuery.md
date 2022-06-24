---
title: JavaScript 6. jQuery (ajax)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JavaScript
description: jQuery
tag : JavaScript Basic
article_tag1: JavaScript
article_section: JavaScript
meta_keywords: JavaScript, css, Front-end
last_modified_at: '2022-06-14 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

jQuery
=========

## 1. 주요 개념

* 화면의 동적 기능을 자바스크립트보다 좀더 쉽고 편리하게 개발할 수 있게 해주는  
  js 라이브러리

### 1) 특징

* css 선택자를 사용해 각 HTML 태그에 접근해서 작업

```js
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.
                                                min.js" ></script>
<script type="text/javascript">
	function fnProcess() {
		let value = $("#textInput").val()
        /* id로 텍스트 박스 접근하여 val()이용해서 입력값 가져옴*/
		$("#textOutput").val(value) 
        /* id로 텍스트 박스 접근하여 val()이용해서 값을 출력함*/ 
	}
</script>
<title>텍스트에 박스 표시</title>
</head>
<body>
	<input type="text" id="textInput" />
	<input type="button" value="입력하기" onclick="fnProcess()" /><br><br>
	결과 : <br>
	<input type="text" id="textOutput" disabled /> 
</body>
```

![alt](/assets/images/post/ajax/3.png)

## 2. 제이쿼리 Ajax 기능

### 1) Asynchronous javascript and XML

* 비동기 통시(클라이언트와 서버 간)으로 데이터를 주고 받기 위한 기술
* XML이나 JSON데이터를 주고 받는 기술. 요즘은 JSON을 주로 사용
* 웹페이지 전체(UI + data)가 아닌 일부(data)만 업데이트 가능

![alt](/assets/images/post/ajax/5.png)

### 2) 사용 형식

```js
    $.ajax({
        type:'post 또는 get',
        url:  "요청 URL",
        dataType: "전송 받을 데이터 타입",
        data: "서버로 전송할 데이터",
        success: function(){
            // 정상 요청, 서버로 부터 응답이 도착하면 호출될 함수
        },
        error: function(){
            // 오류 발생시 처리 
        },
        complete: function(){
            // 작업 완료 후 처리
        }
    })
```

### 3) ajax 실습

* ajax.html

```html
<title>ajax 테스트</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.min.js" ></script>
<script type="text/javascript">
function fnProcess(){
	$.ajax({
		type: "get",
		dataType: "text",	/* 응답 데이터를 텍스트로 지정 */
		url: "http://localhost:8080/chap14_Ajax/ajaxLab",	/* 전송할 서블릿 지정*/
		data: {param:"Hello,jQuery!"},	/* 서버로 매개변수와 값을 설정 */
		success: function(data,textStatus) { /* 전송과 응답이 성공했을경우 작업 설정*/
		    $("#message").append(data)	/* 서버 응답 메세지를 div 엘리먼트에 표신*/
		},
		error: function(data,textStatus){
			alert("에러가 발생했습니다.") /* 작업중 오류 발생했을 경우 수행*/
		},
		complete: function(data,textStatus) {
			alert("작업을 완료했습니다.")	 /*완료시 수행할 작업 설정*/
		}
	})
}
</script>
</head>
<body>
	<input type="button" value="전송하기" onclick="fnProcess()" />
	<div id="message"></div>
</body>
```

* AjaxLab.java

```java
@WebServlet("/ajaxLab")
public class AjaxLab extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, 
    HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		
		String param = request.getParameter("param");	
        // ajax로 전송된 매개변수 가져옴
		System.out.println("From Client : "+param);
		
		PrintWriter out = response.getWriter();
		out.print("안녕하세요. 서버가 보낸 메세지입니다.");	
        // 브라우저(클라이언트)에 응답 메세지 보냄
	}
}

```

![alt](/assets/images/post/ajax/6.png)

### 4) ajax 이용 xml 형식 문서 가져오기

* ajax02.html

```html
<title>ajax 테스트</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.min.js" ></script>
<script type="text/javascript">
	function fnProcess() {
		
	$.ajax({
		type: "post",
		url: "http://localhost:8080/chap14_Ajax/ajaxLab02",
		dataType: "xml",	/* 데이터를 XML형태로 받음*/
		success: function(info, textStatus) {
			$(info).find("book").each(function() {
				/* 전송된 XML 데이터에서 엘리먼트 이름으로 데이터를 가져옴 */
				let title = $(this).find("title").text();
				let writer = $(this).find("writer").text();
				let image = $(this).find("image").text();
				
				/* id가 bookInfo인 div 엘리먼트에 도정보를 표시함 */
				$("#bookInfo").append(
						"<p>"+title+"</p>"+	
						"<p>"+writer+"</p>"+	
						"<img src="+image+"/>"	
				)
				
			})
		}
	})
	}
</script>
</head>
<body>
	<div id="bookInfo"></div>
	<input type="button" value="도서정보 요청" onclick="fnProcess()" />
</body>
</html>
```

* AjaxLab02.java

```java
@WebServlet("/ajaxLab02")
public class AjaxLab02 extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, 
    HttpServletResponse response) throws ServletException, IOException {
		
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=utf-8");
		
		String result = "";
		PrintWriter out = response.getWriter();
		
		// 도서정보를 xml로 작성한 후 클라이언트로 전송
		result = "<main><book>" +
				"<title><![CDATA[Spring Securit 3/e]]></title>" +
				"<writer><![CDATA[믹 넛슨]]></writer>" +
				"<image><![CDATA[http://localhost:8080/chap14_Ajax/image/
                image2.jpg]]></image>" +
				"</book>"+
				"<book>"+
				"<title><![CDATA[함수형 코틀린]]></title>" +
				"<writer><![CDATA[마리오 아리아스]]></writer>" +
				"<image><![CDATA[http://localhost:8080/chap14_Ajax/image/
                image.jpg]]></image>" +
				"</book>"+
				 "</main>";
		System.out.println(result);
		out.print(result);
	}
}
```

![alt](/assets/images/post/ajax/7.png)
![alt](/assets/images/post/ajax/8.png)


### 5) ajax이용 아이디 중복 체크 여부 

* MemberDAO

```java
package kr.co.ezenac.ajax;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;

public class MemberDAO {
	private Connection con;
	private PreparedStatement pstmt;
	private DataSource dataFactory;
	
	public MemberDAO() {
		try {
			Context ctx = new InitialContext();
			Context envContext =(Context) ctx.lookup("java:/comp/env");
			dataFactory =(DataSource) envContext.lookup("jdbc/oracle");
			
			
		}catch(NamingException e) {
			e.printStackTrace();
		}
	}
	
	// 아이디 중복체크 메서드
	public boolean isDuplicated(String id) {
		boolean result = false;
		
		try {
			con = dataFactory.getConnection();
			String query="SELECT DECODE(COUNT(*),1,'true','false') AS result FROM T_MEMBER WHERE id= ?";
			pstmt = con.prepareStatement(query);
			pstmt.setString(1, id);
			ResultSet rs = pstmt.executeQuery();
			
			rs.next();
			result = Boolean.parseBoolean(rs.getString("result"));
			
		}catch(SQLException E) {
			E.printStackTrace();
			System.out.println("ID 중복 여부 체크 중 에러 발생");
		}
		return result;
	}
}

```

* MemberServlet

```java
package kr.co.ezenac.ajax;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/mem")
public class MemberServlet extends HttpServlet {
	@Override
	protected void service(HttpServletRequest request,HttpServletResponse 
	response) throws ServletException, IOException {
		
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=utf-8");
		
		PrintWriter out = response.getWriter();
		
		String id = request.getParameter("id");
		System.out.println("id = "+id);
		
		MemberDAO dao = new MemberDAO();
		boolean isDuplicated = dao.isDuplicated(id);
		
		if(isDuplicated == true) {
			out.print("not_usable");	// true면 중복된 아이디
		}
		else {
			out.print("usable");
		}
	}
}

```

* ajax.html

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>ajax 테스트 - 아이디 중복 체크</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/
											jquery.min.js" ></script>
<script type="text/javascript">
	function fnProcess() {
		let _id = $("#tId").val()
		if(_id == ''){
			alert("ID를 입력하세요")
			return
		}
	$.ajax({
		type : "post",
		url : "http://localhost:8080/chap14_Ajax/mem",
		dataType:"text",
		data:{id: _id}, /* ID를 서블릿으로 전송 */
		success: function(data,textStatus) {	
			/* 서버에서 전송된 결과에 따라 메세지 표시 */
			if(data == 'usable'){
				$('#message').text('사용할수 있는 아이디 이다.')
				$('#btnDuplicate').prop("disabled",true)	
				/* 버튼을비활성화 시킴 */
			}
			else{
				$('#message').text('중복된 아이디 입니다.')
			}
			},
			error: function(data,textStatus) {
				alert("에러가 발생했습니다.")
			},
			complete: function(data,textStatus) {
				alert("작업을 완료했습니다.")
			}	
		})
	}
</script>
</head>
<body>
	<input type="text" id="tId" />
	<input type="button" id="btnDuplicate" value="ID 중복체크하기" onclick="fnProcess()" />
	<div id="message"></div>
</body>
</html>
```

![alt](/assets/images/post/ajax/9.png)

## 3. 제이쿼리에서 JSON 사용하기

### 1) Java Script Object Notation

* 자바스크립트 객체 표기법

### 2) {속성명1:속성값2, 속성명2:속성값2, ...}

```json
 [{속성명1:속성값2, 속성명2:속성값2,..},
 {속성명1:속성값2, 속성명2:속성값2}]	// 객체배열
	
{키1:{속성명1:속성값2, 속성명2:속성값2},...},
{키2:{속성명1:속성값2, 속성명2:속성값2},...} // map
```

* name/value 쌍으로 이루어진 데이터를 전달하기 위해 인간이 읽을 수 있는  
  텍스트를 사용하는 개방형 표준 데이터 형식
* 비동기 브라우저/서버 통신(Ajax)을 위해 XML을 대체하는 데이터 전송형식
* 프로그래밍 언어나 플랫폼에 독립적이어서 쉽게 사용가능
* JS객체를 서버로 전송하려면, 직렬화가 필요함
	* JS객체 -> 문자열로 변환 
* 서버가 보낸 데이터(JSON 문자열)를 JS객체로 변환할 때, 역직렬화가 필요
	* 문자열 -> JS객체로 변환

```json
	{name: "kim",age : 30}	--->	'{"name":"kim","age":30}'
	---------------------	<---	 -----------------------
			JS 객체			JSON.parse()	 String
```
* json.jsp

```html
<script type="text/javascript">
	$(function() {
		$("#checkJson").click(function() {
			let jsonStr = '{"name":["이순신","신사임당","이도"]}' 
			/* json 배열을 name이름으로 저장 */
			let jsonInfo = JSON.parse(jsonStr)				
			/* JSON 자료형을 리턴 */
			
			let output="회원 정보<br>"
			output += "===============<br>"
			for(let i in jsonInfo.name){
				/* 배열이름 name으로 배열 요소에 반복변수 이용해 값을 가져옴*/
				output += jsonInfo.name[i] + "<br>"
			}
			$("#output").html(output) /* 회원이름 출력 */
		})
	})
</script>
<title>JSON 테스트</title>
</head>
<body>
	<a id="checkJson" style="cursor: pointer;">출력</a><br><br>
	<div id="output"></div>
```

![alt](/assets/images/post/ajax/10.png)

* 회원 정보 출력
* json03.jsp

```js
	$(function() {
		$("#checkJson").click(function() {
							/* 회원정보 */
			let jsonStr = '{"name":"정원영","age":26,"gender":"남자","nickname":"BOB"}'
			let jsonInfo = JSON.parse(jsonStr)/* JSON 자료형을 리턴 */
			let output="회원 정보<br>"
			output += "===============<br>"
			output += "이름: " +jsonInfo.name+"<br>" 
			/* 문자열에서 JSON객체 속성 가져옴 */
			output += "나이: " +jsonInfo.age+"<br>"
			output += "성별: " +jsonInfo.gender+"<br>"
			output += "별명: " +jsonInfo.nickname+"<br>"
			
			$("#output").html(output) /* 회원이름 출력 */
		})
	})
```

![alt](/assets/images/post/ajax/11.png)

### 3) 배열로 받기 

* json04.jsp

```js
	$(function() {
		$("#checkJson").click(function() {
			/* members 배열에 회원정보 객체의 name/value 쌍으로 저장 */
			let jsonStr = '{"members":[{"name":"정원영","age":26,"gender":"남자","nickname":"BOB"},{"name":"개발자 정원영","age":25,"gender":"남자","nickname":"BOBdev"}]}'
			let jsonInfo = JSON.parse(jsonStr)	/* JSON 자료형을 리턴 */
			
			let output="회원 정보<br>"
			output += "===============<br>"
			for(let i in jsonInfo.members){
			output += "이름: " +jsonInfo.members[i].name+"<br>" /* 문자열에서 JSON객체 속성 가져옴 */
			output += "나이: " +jsonInfo.members[i].age+"<br>"
			output += "성별: " +jsonInfo.members[i].gender+"<br>"
			output += "별명: " +jsonInfo.members[i].nickname+"<br><br>"

			}
			$("#output").html(output) /* 회원이름 출력 */
		})
	})
```

![alt](/assets/images/post/ajax/12.png)

### 4) 클라이언트 -> 서버로 전송

* json05.jsp

```js
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.
									min.js" ></script>
<script type="text/javascript">
	$(function() {
		$("#checkJson").click(function() {
			/* 전송할 회원정보를 JSON 형식으로 만듬*/
			let _jsonInfo = '{"name":"정원영","age":26,"gender":"남자","nickname":"BOB"}'
			$.ajax({
				type: "post",
				url: "${contextPath}/json",
				data: {jsonInfo: _jsonInfo}, 
				/* 매개변수 이름 jsonInfo로 JSON데이터를 ajax로 전송*/
				success: function(data,textStatus) {},
				error: function(data,textStatus) {alert("에러가 발생했습니다.")},
				complete: function(data,textStatus) {alert("작업을 완료했습니다.")}
			})
		})
	})
```

* JsonServlet.java

```java
@WebServlet("/json")
public class JsonServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=utf-8");
		
		// 문자열로 전송된 JSON 데이터를 가져옴
		String jsonInfo = request.getParameter("jsonInfo");
		
		// JSON데이터를 처리하기위해 JSONParser객체 생성
		JSONParser jsonParser = new JSONParser();
		try {
			//전송된 JSON 데이터를 파싱
			JSONObject jsonObject =(JSONObject) jsonParser.parse(jsonInfo);
			
			System.out.println("회원 정보");
			// JSON 데이터의 name속성들을 get()전달해 value 출력함.
			System.out.println(jsonObject.get("name"));
			System.out.println(jsonObject.get("age"));
			System.out.println(jsonObject.get("gender"));
			System.out.println(jsonObject.get("nickname"));
		} catch (ParseException e) {
			
			e.printStackTrace();
		}
	}
}

```

![alt](/assets/images/post/ajax/13.png)