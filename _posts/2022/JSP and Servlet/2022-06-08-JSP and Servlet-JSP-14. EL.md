---
title: JSP 14. EL
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JSP and Servlet
description: JSP
tag : EL
article_tag1: JSP
article_section: JSP
meta_keywords: java,java JSP, JDBC
last_modified_at: '2022-06-08 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

EL
===

## 1. 표현언어 (EL : Expression Language)소개

* 변수의 값을 표현식(<%= %>)보다 편하게 출력가능

```jsp
    ${값 or 속성 or 표현식}
```

* JSP의 기본 문법을 보완
* 4가지 영역에 저장된 속성 더 쉽게 읽을 수 있음
* 모델2 방식으로 웹 어플리케이션을 개발할 때 주로 사용됨
* HTML 태그나 자바스크립트, CSS 어디에서든 사용가능
* 메서드 호출

```jsp
<body>
	<h1>
		${100 }<br>
		${"좋은 목요일 입니다." } <br>
		${10+1 }<br>
		${"10" +1 }<br>		
        <!--숫자형 문자열과 실제문자로 더하면 문자열이 자동으로 숫자로 변환 -->
		${null + 10 }		<!--  null 변수사용하면 예외가 발생하지 않음 -->
	</h1>
	
</body>
```

![alt](/assets/images/post/jsp/104.png)

### 산술, 비교, 논리 연산이 가능

#### 1) 산술 연산자 

* +,-,*
* / 또는 div
* % 또는 mod

#### 2) 비교 연산자

* ```>``` 또는 gt
* ```>=``` 또는 ge
* < 또는 lt
* <= 또는 le
* == 또는 eq
* != 또는 ne

#### 3) 논리 연산자

* && 또는 and
* || 또는 or
* ! 또는 not

#### 4) empty 연산자

* 값이 없을때 true 반환하는 연산자

* null
* 빈 문자열
* 길이가 0인 배열
* size가 0인 컬렉션

#### 5) 삼항 연산자

* ${조건 ? "true일때 선택" : "false일때 선택"}

```jsp
<%
	// 변수 선언
	pageContext.setAttribute("num1", 9);
	pageContext.setAttribute("num2", "10");
	pageContext.setAttribute("nullStr", null);
	pageContext.setAttribute("emptyStr", "");
	pageContext.setAttribute("lengthZero", new Integer[0]);
	pageContext.setAttribute("sizeZero", new ArrayList());
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>el - 연산자 </title>
</head>
<body>
	${numberVar = 10 }			<!-- 할당과 동시에 출력 -->
	${numberVar = 10;''  }<br>	<!-- 할당만 되고 출력은 되지 않음 -->
	
	<h3>empty 연산자</h3>
	empty nullStr : ${empty nullStr }<br/>
	empty emptyStr : ${empty emptyStr }<br/>
	empty lengthZero : ${empty lengthZero }<br/>
	empty sizeZero : ${empty sizeZero }<br>
	
	<h3>삼항 연산자</h3>
	num1 gt num2 ? "참" : "거짓" => ${num1 gt num2 ? "num1이 크다 (참)" :"num2가 크다 (거짓)" }
	
	<h3>null 연산</h3>
	null + 10 : ${null + 10 } <br/>		<!-- null은 모두 0으로 처리됨 -->
	nullStr + 10 : ${nullStr + 10 }<br>
</body>
```

![alt](/assets/images/post/jsp/111.png)


## 2. EL의 내장 객체 (스코프)

### 1) pageScope

* pageContext 내장 객체와 같이 page 영역에 저장된 속성값을 읽어옴

### 2) requestScope

* request 내장 객체와 같이 request 영역에 저장된 속성값을 읽어옴

### 3) sessionScope

* session 내장 객체와 같이 session 영역에 저장된 속성값을 읽어옴

### 3) applicationScope

* application내장 객체와 같이 application 영역에 저장된 속성값을 읽어옴

### 4) main 화면

```jsp
<%

	int num1 = 3;
	// 4가지 영역 모두에 "scopeValue"라는 같은 이름으로 속성을 저장함
	pageContext.setAttribute("scopeValue", "페이지 영역");
	request.setAttribute("scopeValue", "리퀘스트 영역");
	session.setAttribute("scopeValue", "세션 영역");
	application.setAttribute("scopeValue", "애플리케이션 영역");
	
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>표현 언어(EL) - 내장 객체</title>
</head>
<body>
	<h2>각 영역에 저장된 속성 읽기(EL 내장 객체 사용)</h2>
	<!--  EL의 내장 객체를 통해 각 영역에 저장된 속성값 출력 -->
	<ul>
		<li>스크립트릿에서 선언한 변수 : ${num1 }</li>
		<li>페이지 영역(EL) : ${pageScope.scopeValue }</li>
		<li>리퀘스트 영역(EL) : ${requestScope.scopeValue }</li>
		<li>세션 영역(EL) : ${sessionScope.scopeValue }</li>
		<li>애플리케이션 영역(EL) : ${applicationScope.scopeValue }</li>
	</ul>
	
	<h2>영역 지정없이 속성 읽기</h2>
	<ul>
	<!-- 영역을 따로 지정하지 않으면 가장 좁은 영역에서 부터 속성을 찾는다. -->
		<li>${scopeValue }</li>
	</ul>
</body>
```

![alt](/assets/images/post/jsp/105.png)

### 5) foward 페이지

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>표현 언어(EL) - 내장 객체</title>
</head>
<body>
	<h2>각 영역에 저장된 속성 읽기(EL 내장 객체 사용)</h2>
	<!--  내장 객체의 영역중 page 영역은 포워드되면 소멸되고 새로 만들어짐 -->
	<ul>
		<li>스크립트릿에서 선언한 변수 : ${num1 }</li>
		<li>페이지 영역(EL) : ${pageScope.scopeValue }</li>
		<li>리퀘스트 영역(EL) : ${requestScope.scopeValue }</li>
		<li>세션 영역(EL) : ${sessionScope.scopeValue }</li>
		<li>애플리케이션 영역(EL) : ${applicationScope.scopeValue }</li>
	</ul>
	
	<h2>영역 지정없이 속성 읽기</h2>
	<ul>
	<!-- 영역을 따로 지정하지 않으면 가장 좁은 영역에서 부터 속성을 찾는다. -->
		<li>${scopeValue }</li>
	</ul>
</body>
</html>
```

![alt](/assets/images/post/jsp/106.png)

## 3. 폼값 처리하기 (요청 매개변수)

* jsp에서는 전송방식(get/post)에 상관없이 request.getParameter()로 폼값 받음

### 폼값 처리위한 내장 객체

#### 1) param

* request.getParameter("매개변수명")와 동일함

#### 2) paramValues

* request.getParameterValues("매개변수명")와 동일함

#### 3) formParamSubmit.jsp

```jsp
<body>
	<h2>폼값 처리</h2>
	<form action="formParamResult.jsp" method="post">
		이름 : <input type="text" name="name" /><br/>
		성별 : <input type="radio" name="gender" value="man" />남자
			  <input type="radio" name="gender" value="woman" />여자<br/>
	    학력 : 
			  <select name="grade">
			  	<option value="ele">초등</option>
			  	<option value="mid">중등</option>
			  	<option value="high">고등</option>
			  	<option value="uni">대학</option>
			  </select><br/>
		관심 사항 : 
			<input type="checkbox" name="interest" value="pol" />정치
			<input type="checkbox" name="interest" value="eco" />경제
			<input type="checkbox" name="interest" value="ent" />연애
			<input type="checkbox" name="interest" value="spo" />운동<br/>
		<input type="submit" value="전송하기" />
	</form>
</body>
```

![alt](/assets/images/post/jsp/107.png)

#### 4) formParamResult.jsp

```jsp
<h3>EL로 폼값 받기</h3>
	<ul>
		<li>이름 : ${param.name }</li>
		<li>성별 : ${param.gender }</li>
		<li>학력 : ${param.grade }</li>
		<li>관심사항 : ${paramValues.interest[0]}
					${paramValues.interest[1]}
					${paramValues.interest[2]}
					${paramValues.interest[3]}
		</li> 
	</ul>
```

![alt](/assets/images/post/jsp/108.png)

## 4. 객체 전달하기

### 1) 폼으로는 객체 전송 불가

### 2) 영역(Scope)을 사용해서 객체 전송 가능
* 객체를 영역에 저장한 후 => 내장 객체의 영역이 공유됨   
                                =>    전송하고자 하는 페이지 전달

#### person.java

```java
package kr.co.ezenac.el;

public class Person {
	private String name;
	private int age;
	
	public Person() {}
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
}
```

#### objectParam.jsp

```jsp
<body>
	<%
		/* Person 객체 생성 후 request 영역에 저장함 */
		request.setAttribute("personObj", new Person("이순신", 33));
		request.setAttribute("stringObj", "나는 문자열입니다.");
		request.setAttribute("integerObj", new Integer(100));
	%>
	<!--  액션 태그 이용 ObjectResult.jsp로 포워딩 -->
	<!--  포워드된 페이지로 전달 -->
	<jsp:forward page="objectResult.jsp">
		<jsp:param value="10" name="firstNum"/>	
		<jsp:param value="20" name="secondNum"/>
	</jsp:forward>
</body>
```

#### objectResult.jsp

```jsp
<body>
	<h2>영역을 통해 전달된 객체 읽기</h2>
	<ul>
		<li>Person 객체 => 이름 : ${personObj.name }, 나이 : ${personObj.age }</li>
		<li>String 객체 => ${requestScope.stringObj }</li>
		<li>Integer 객체 => ${integerObj }</li>
	</ul>
	
	<h2>매개변수로 전달된 값 읽기</h2>
	<ul>
		<li>${param.firstNum + param.secondNum}</li>
		<li>${param.firstNum }+ ${param.secondNum }</li>
	</ul>
</body>  
```
![alt](/assets/images/post/jsp/109.png)

## 5.쿠키,HTTP헤더,컨텍스트 초기화 매개변수 출력하기

* cookie : 쿠키를 읽을 때 사용
* header : 헤더값 읽을 때 사용
* headerValues : 헤더값 배열 형태로 읽음
* initParam : web.xml에 설정된 컨텍스트 초기화 매개변수 읽을 때 사용
* pageContext : JSP의 pageContext 내장 객체와 동일 역할

### 1) ImplicitObjOthers.jsp

```jsp
<%@page import="kr.co.ezenac.el.CookieManager"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	CookieManager.makeCookie(response, "ELCookie", "쿠키입니다.", 10);
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>표헌 언어 - 그외 내장 객체</title>
</head>
<body>
	<h3>쿠키값 읽기</h3>
	<li>EL Cookies 값 : ${cookie.ELCookie.value }</li>
	
	<h3>HTTP 헤더 읽기</h3>
	<ul>
		<li>host: ${header.host} </li>
		<li>user-agent : ${header['user-agent'] }</li>
		<li>cookie : ${header.cookie }</li>
	</ul>
	
	<h3>컨텍스트 초기화 매개변수 읽기</h3>
	<li>OracleDriver : ${initParam.OracleDriver } </li>
	
	<h3>컨텍스트 루트 경로 읽기</h3>
	<li>${pageContext.request.contextPath }</li>
</body>
</html>
```

![alt](/assets/images/post/jsp/110.png)

## 6. 빈사용

### 1) 빈 속성 접근 방법

* ${빈이름.속성이름}

## 7. Collection 객체 사용

### 1) 접근형식

* ${collection객체이름[index].속성이름}
* ${hashMap객체이름.키이름}

```jsp
	...
<% request.setCharacterEncoding("utf-8"); %>
<jsp:useBean id="m1" class="kr.co.ezenac.el.MemberBean" />
<jsp:setProperty property="*" name="m1"/>
<jsp:useBean id="membersList" class="java.util.ArrayList" />
	<!-- 회원정보를 저장한 HashMap 객체를 액션태그 이용해 생성 -->
<jsp:useBean id="membersMap" class="java.util.HashMap" />

<%
	/* HashMap에 key/value 쌍으로 회원정보 저장 */
   membersMap.put("id","bobDeveloper"); 
   membersMap.put("pwd","0824");
   membersMap.put("name", "정원영님");
   membersMap.put("email","nicednjsdud2@naver.com");
   
   /* 회원정보 저장하는MemberBean 객체 생성*/
	MemberBean m2 = new MemberBean("nicednjsdud","0824","BOB","nicednjsdud@naver.com");
   
   /* 전송된 회원정보(m1)와 자바코드로 생성한 회원정보(m2)를 ArrayList에 저장 */
   membersList.add(m1);
   membersList.add(m2);
   
   /* 회원정보가 저장된 memberList를 memberList라는 key로 Hashmap에 저장 */
   membersMap.put("membersList",membersList);
%>
	...
	...
<body>
	<table border="1" align="center">
		<tr align="center" bgcolor="#99ccff">
			<td width=20%><b>아이디</b></td>
			<td width=20%><b>비밀번호</b></td>
			<td width=20%><b>이름</b></td>
			<td width=20%><b>이메일</b></td>
		</tr>
<!-- HashMap이름 뒤에 .연산자로 저장시 사용한 key를 사용하여value를 가져옴 -->
		<tr align="center">
			<td>${membersMap.id }</td>
			<td>${membersMap.pwd }</td>
			<td>${membersMap.name }</td>
			<td>${membersMap.email }</td>
		</tr>
<!-- HashMap이름 뒤에 저장된 ArrayList에 .연산자로 접근한 후 다시 각각의
 속성에 .를 이용해 첫번째 회원정보 접근-->
		<tr align="center">
			<td>${membersMap.membersList[0].id }</td>
			<td>${membersMap.membersList[0].pwd }</td>
			<td>${membersMap.membersList[0].name }</td>
			<td>${membersMap.membersList[0].email }</td>
		</tr>
<!-- HashMap이름 뒤에 저장된 ArrayList에 .연산자로 접근한 후 다시 각각의 
속성에 .를 이용해 두번째 회원정보 접근-->
		<tr align="center">
			<td>${membersMap.membersList[1].id }</td>
			<td>${membersMap.membersList[1].pwd }</td>
			<td>${membersMap.membersList[1].name }</td>
			<td>${membersMap.membersList[1].email }</td>
		</tr>
	</table>
</body>
</html>
```

![alt](/assets/images/post/jsp/112.png)

## 8. has-a 관계 빈 사용

### 1) 접근 형식

#### ${부모빈이름.자식속성이름.속성이름}
* MemberBean객체의 address객체 추가

* Address.java

```java
public class Address {
	private String city;
	private String zipcode;
	
	public Address() {}
	public String getCity() {return city;}
	public void setCity(String city) {this.city = city;}
	public String getZipcode() {return zipcode;}
	public void setZipcode(String zipcode) {this.zipcode = zipcode;}
}
```

* MemberBean.java

```java
	...
private String email;
	private Date joinDate;
	private Address addr;// 주소 정보를 저장하는 Address 클래스 타입 속성 선언
		
	public MemberBean() {}
	...
	public Address getAddr() {return addr;}
	public void setAddr(Address addr) {this.addr = addr;}
```

```jsp
<% request.setCharacterEncoding("utf-8"); %>
<jsp:useBean id="m" class="kr.co.ezenac.el.MemberBean" />
<jsp:setProperty property="*" name="m"/>
	<!-- address빈을 생성한후 도시와 우편번호 설정 -->
<jsp:useBean id="addr" class="kr.co.ezenac.el.Address" />
<jsp:setProperty property="city" name="addr" value="화성" />
<jsp:setProperty property="zipcode" name="addr" value="18394"/>
<!-- MemberBean의 addr 속성에 Address빈을 설정 -->
<% m.setAddr(addr); %>
	...
	...
		<!-- 자바빈의 속성이름과 .연산자를 이용해 주소 출력 -->
		<tr align="center">
			<td>${m.id }</td>
			<td>${m.pwd }</td>
			<td>${m.name }</td>
			<td>${m.email }</td>
			<td>${m.addr.city }</td>
			<td>${m.addr.zipcode }</td>
		</tr>
	</table>
</body>
```

![alt](/assets/images/post/jsp/113.png)

## 9. 인스턴스 ,정적 메서드 호출

* Elclass.java

```java
package kr.co.ezenac.el;

public class ELClass {
	
	// 주민번호를 입력받아 성별을 반환함
	public String getGender(String jumin) {
		String returnStr="";
		
		int beginIdx = jumin.indexOf("-")+1;
		String genderStr = jumin.substring(beginIdx, beginIdx+1);
		
		int genderInt = Integer.parseInt(genderStr);
		if(genderInt==1|genderInt==3)
				returnStr ="남자";
		else if(genderInt==2||genderInt==4)
				returnStr ="여자";
		else
			returnStr="입력오류";
		
		return returnStr;
		}
	// 입력받은 정수까지의 구구단을 Html 테이블로 출력
	public static String showGugudanEx(int dan) {
		StringBuffer sb = new StringBuffer();
		
		sb.append("<table border=1>");
		
		for(int i=2;i<=dan;i++) {
			sb.append("<tr>");
			for(int j=1;j<=9;j++) {
				sb.append("<td>"+i+"*"+j+"="+(i*j)+"</td>");
			}
			sb.append("</tr>");
		}
		
		sb.append("</table>");
		
		return sb.toString();
	}
}

```

* ELCLassMethodCall.jsp

```jsp
...
<%
	ELClass elclass = new ELClass();
	pageContext.setAttribute("elclass", elclass);	//page영역에 저장
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>EL - 메서드 호출</title>
</head>
<body>
	<h3>영역에 저장후 메서드 호출</h3>
	220610-3225567 => ${elclass.getGender(220610-3225567) }<br>
	220610-2225567 => ${elclass.getGender(220610-2225567) }<br>
	<h3>클래스명을 통해 정적 메서드 호출</h3>
	${ELClass.showGugudanEx(7) }
</body>
</html>
```

![alt](/assets/images/post/jsp/115.png)