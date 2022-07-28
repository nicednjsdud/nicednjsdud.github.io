---
title: (Spring) 9. 스프링 어노테이션 종류들
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: 스프링 어노테이션 종류들
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-12 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Spring Annotation

## 1. 소개

- 기존에 XML에서 빈 설정을 에노테이션을 이용해서 자바 코드에서 설정하는 방법
- 기능이 복잡해짐에 따라 XML에서 설정하는 것보다 유지보수에 유리함.
- 현재 애플리케이션 개발시 XML 설정 방법과 애너테이션 방법을 혼합해서 사용함.

![alt](/assets/images/post/spring/23.png)

## 2. Bean 등록 메타정보 구성 전략

### 1) XML 단독 사용

- 모든 Bean을 명시적으로 XML에 등록 하는 방법

### 2) XML과 빈 스캐닝 (Bean Scanning)의 혼용

- Bean으로 사용될 클래스에 특별한 애노테이션을 부여해주면 이런 클래스를  
  자동으로 찾아서 Bean으로 등록함.

  - 빈 스캐닝을 통한 자동인식 Bean 등록기능이라고 함.

- Annotation을 부여하고 자동으로 빈을 등록하면 개발속도 향상시킴

## 3. annotation-based programming

- @Controller, @RequestMapping 등 다양한 애노테이션을 제공함
- 애노테이션을 통한 요청 연결, 데이터 가공, 예외 처리 등 구성함

## 4. annotation

- 코드의 메타-데이터(Metadata)로 작성, 컴파일 또는 런타임에 활용됨
- JDK가 제공하는 빌트인(Built-in)과 직접 작성하는 커스텀(Custom)으로 분류됨.
- 패키지, 클래스, 메소드, 필드에 선언할 수 있음.
- `@{AnnotationName}` 으로 표기함

## 5. 스프링 애너테이션 제공 클래스

### 1) 브라우저 URL 요청처리 애너테이션 관련 클래스

#### 1.1 DefaultAnnotationHandlerMapping

- 클래스 레벨에서 `@RequestMapping`을 처리함

#### 1.2 AnnotationMethodHandlerAdapter

- 메서드 레벨에서 `@RequestMapping`을 처리함

## 5. `<context:component-scan>`태크

- 패키지 이름을 지정하면 애플리케이션 실행 시 해당 패키지에서 애너테이션으로 지정된  
  클래스를 빈으로 만들어줌.

### 1) 사용 형식

```
    <context:component-scan base-package="패키지 이름" />
```

## 6. 여러가지 스테레오 타입 애너테이션

- @Controller @Service @Repository는 @Component의 구체화된,  
  더특정한 유즈케이스된 형태임.

### 1) @Controller

- 프리젠테이션 레이어, 웹 애플리케이션에서 웹 요청과 응답을 처리하는 클래스
- 스프링 컨테이거가 component-scan에 의해 지정한 클래스를 컨트롤러 빈으로  
  자동 변환함.
- Controller 클래스 정의

### 2) @Service

- 서비스 레이어, 비즈니스 로직을 가진 클래스
- 스프링 컨테이거가 component-scan에 의해 지정한 클래스를 서비스 빈으로  
  자동 변환함.

### 3) @Repository

- 퍼시스턴스(persostence) 레이어, 영속성을 가지는 속성(파일, DB)을 가진 클래스
- 스프링 컨테이거가 component-scan에 의해 지정한 클래스를 DAO 빈으로  
  자동 변환함.

### 4) @Component

- 컴포넌트를 나타내는 일반적인 스테레오 타입으로 `<bean>`태그와 동일한 역할을 함
- 스프링 컨테이거가 component-scan에 의해 지정한 클래스를 빈으로  
  자동 변환함.

## 7. 관련 애노테이션

### 1) @RequestMapping

- URL 주소를 맵핑
- HTTP 요청 URL을 처리할 Controller 정의

### TEST

#### 1. web.xml 변경

- 기본 root-context.xml과 appServlet/servlet-context.xml을 사용하지않고  
  action-servelt.xml에 따라 정의해 보았다.

##### Web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
    https://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">


	<!-- Creates the Spring Container shared by all Servlets and Filters -->
	<!-- 여러 설정 파일을 읽어들이기 위해 스프링의 ContextLoaderListener을 설 -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>

	<!-- 애플리케이션 실행시 ContextLoaderListener로 해당 위치의 설정 파일을 읽어 들 -->
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/config/action-mybatis.xml</param-value>
	</context-param>

	<!-- Processes application requests -->
	<servlet>
		<servlet-name>action</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<load-on-startup>1</load-on-startup>
	</servlet>

	<servlet-mapping>
		<servlet-name>action</servlet-name>
		<url-pattern>*.do</url-pattern>
	</servlet-mapping>

</web-app>

```

#### 2. config/mybatis.xml 생성

- Default인 servlet-context.xml 대신 config/action-mybatis.xml을 넣었다.

##### action-mybatis

- WEB-INF폴더 밑 config 폴더 생성후 action-mybatis.xml 생성

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.1.xsd
		http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx-3.1.xsd">

	<!-- PropertyPlaceholderConfigurer 클래스 이용해 db 설정 관련 정보를 jdbc.properties 파일에서 읽어 들임 -->
	<bean id="propertyPlaceholderConfigurer"
					class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
		<property name="locations">
			<value>/WEB-INF/config/jdbc.properties</value>
		</property>
	</bean>

	<!-- PooledDataSource 이용해서 dataSource 빈 생성 -->
	<bean id="dataSource" class="org.apache.ibatis.datasource.pooled.PooledDataSource">
		<property name="driver" value="${jdbc.driverClassName}" />
		<property name="url" value="${jdbc.url}"/>
		<property name="username" value="${jdbc.username}"/>
		<property name="password" value="${jdbc.password}"/>
	</bean>


	<!-- DataSourceTransactionManager클래스를 이용해 dataSource 빈에 트랜잭션을 적용함 -->
	<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource" />
	</bean>

	<!-- 애너테이션을 사용하여 트랜잭션을 적용하기 위해 txManager 빈을 설정함 -->
	<tx:annotation-driven transaction-manager="txManager" />
</beans>
```

##### jdbc.properties 생성

- db 연동을 위한 파일이다.

```
jdbc.driverClassName=oracle.jdbc.driver.OracleDriver(오라클)
jdbc.url=[jdbc URL]
jdbc.username=[유저아이디]
jdbc.password=[유저비밀번호]
```

#### 3. action-servlet.xml 생성

- default인 servlet-context을 쓰지않고 action-servlet을 생성해 사용

##### action-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop-3.1.xsd
		http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.1.xsd">

	<bean id="viewResolver"
		class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="viewClass"
			value="org.springframework.web.servlet.view.JstlView" />
		<property name="prefix" value="/WEB-INF/views/anno/" />		<!-- jsp 파일 위치 지정 -->
		<property name="suffix" value=".jsp" />
	</bean>
	<!-- 클래스 레벨에 @RequestMapping을 처리함 -->
	<bean
		class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping" />

	<!-- 메서드 레벨에 @RequestMapping을 처리함 -->
	<bean
		class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter" />

	<!-- kr.co.annotation 패키지에 존재하는 클래스에 애너테이션이 적용되도록 설정함 -->
	<context:component-scan base-package="kr.co.bob" />
</beans>

```

#### 4. MainController.java 생성

```java
package kr.co.bob.anno01;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller("mainController")
// @Controller 애너테이션을 이용해 MainController 클래스를 빈으로 자동 변환함. 빈id는 mainConroller임
@RequestMapping("/anno")
// @RequestMapping을 이용해 첫번째 단계의 URL 요청이 /anno이면 mainController 빈을 요청
public class MainController {

	@RequestMapping("/main1.do")
	// @RequestMapping을 이용해 두번째 단계의 URL요청이 /main1.do이면 mainController의 bob1에게 요청
	public ModelAndView bob1(HttpServletRequest request, HttpServletResponse response)
                                     throws Exception {
		ModelAndView mav = new ModelAndView();
		mav.addObject("msg","It's BOBWorld !");
		mav.setViewName("main");
		return mav;
	}
}
```

#### 5. main.jsp 생성

- 요청을 /anno/main.jsp로 했기때문에 anno폴더 생성후 main.jsp를 생성해준다.

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%> <% request.setCharacterEncoding("utf-8"); %>
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>결과</title>
  </head>
  <body>
    <h1>2022년 7월입니다.</h1>
    <h1>${msg }</h1>
    <!-- 컨틀롤러에서 넘긴 메세지를 출력 -->
  </body>
</html>
```

#### 6. 결과

![alt](/assets/images/post/spring/24.png)

### 2) @RequestParam

- 매개변수 갯수가 많아지면 일일이 getParameter()를 이용하는 방법은 불편함
- 메서드에 적용해 쉽게 값을 얻을 수 있음
- HTTP 요청에 포함된 파라미터 참조 시 사용

#### 1.1 적용 시 **required** 속성을 생략하면 기본값은 **true** 이다.

- 메서드 호출 시 반드시 지정한 이름의 매개변수를 전달해야 함.
- 매개변수가 없으면 예외가 발생
- required 속성을 **false**로 설정하면 메서드 호출 시 지정한 이름의 매개변수가  
  전달되고, 없으면 **null**을 할당함.

![alt](/assets/images/post/spring/26.png)

#### 1.2 Mapa에 매개변수 값 설정하기

- 전송되는 매개변수 수가 많을 경우 Map에 바로 저장해서 사용

### TEST

#### 1. loginForm.jsp에서 정보 입력후 전송

- jsp폼으로 회원아이디, 비밀번호 login2.do로 전송

```html
...
<form name="frmLogin" method="post" action="${contextPath }/anno/login2.do">
  ...
  <!-- @RequestParam에 설정한 userId와 같아야 함 -->
  <td><input type="text" name="userId" size="20" /></td>
  <!-- @RequestParam에 설정한 userName 같아야 함 -->
  <td><input type="text" name="userName" size="20" /></td>
  ...
</form>
```

#### 2. loginController에 메서드 추가

##### 1. 일반적인 방법 @RequestParam 에너테이션으로 하나씩 받아옴

```java
/*
	 *  @RequestParam을 이용해 매개변수가 userId이면 그값을 변수 userId에 자동으로 설정
	 *  @RequestParam을 이용해 매개변수가 userName이면 그값을 변수 userName에 자동으로 설정
	 */
	@RequestMapping(value= "/anno/login2.do", method = {RequestMethod.GET ,RequestMethod.POST})
	public ModelAndView login2(
            @RequestParam("userId") String userId,@RequestParam("userName") String userName,
				HttpServletRequest request,HttpServletResponse response)throws IOException{
		request.setCharacterEncoding("UTF-8");
		ModelAndView mav = new ModelAndView();
		mav.setViewName("result");
		mav.addObject("userId",userId);
		mav.addObject("userName",userName);
		return mav;
	}
```

- Map을 통해서 폼에서 name=key value=value로 가져옴

```java
	/*
	 *  @RequestParam 이용해 Map에 전송된 매개변수 이름을 key, 값이 value로 저장
	 */
	@RequestMapping(value= "/anno/login2.do", method = {RequestMethod.GET ,RequestMethod.POST})
	public ModelAndView login3(@RequestParam Map<String,String> info,
			HttpServletRequest request,HttpServletResponse response)throws IOException{

		request.setCharacterEncoding("UTF-8");
		ModelAndView mav = new ModelAndView();

		// @RequestParam에서 설정한 Map 이름으로 바인딩함.
		mav.addObject("info",info);
		mav.setViewName("result");

		return mav;
	}
```

#### 3. result.jsp 생성

```html
...
<body>
  <!-- 일반적인 방법으로 했을 때  -->
  <h1>아이디: ${userId }</h1>
  <h1>이름 : ${userName }</h1>

  <!-- Map을 이용하여 했을 때 -->
  <h1>아이디: ${info.userId }</h1>
  <h1>이름 : ${info.userName }</h1>
</body>
...
```

#### 4. 결과

![alt](/assets/images/post/spring/25.png)

### 3) @ModelAttribute

- HTTP 요청에 포함된 파라미터를 모델 객체로 바인딩

### TEST

#### 1. LoginDTO.java 생성

- DTO에 접근하여 바인딩을 하므로 LoginDTO가 필요하다.

```java
public class LoginDTO {
	private String userId;
	private String userName;

    // 게터 세터 추가
}
```

#### 2. LoginController 메서드 생성

- @ModelAttribute를 이용하여 LoginDTO 를 가져옴

```java
/*
	 *  @ModelAttribute를 이용해 전달되는 매개변수 값을 LoginDTO 클래스와 이름이 같은 속성에 자동으로 설정함
	 *  addObject() 이용할 필요없이 info를 이용해 바로 JSP에서 LoginDTO 속성에 접근할 수 있음.
	 *
	 */
	@RequestMapping(value="/anno/login2.do",method= {RequestMethod.GET,RequestMethod.POST})
	public ModelAndView login2(@ModelAttribute("info") LoginDTO loginDTO,
				HttpServletRequest request,HttpServletResponse response) throws IOException{
		request.setCharacterEncoding("UTF-8");
		ModelAndView mav = new ModelAndView();
		mav.setViewName("result");
		return mav;
    }
```

#### 3. result.jsp 생성

```html
...
<body>
  <!-- @ModelAttribute("info") 에서 지정한 이름으로 속성에 접근함-->
  <h1>아이디: ${info.userId }</h1>
  <h1>이름 : ${info.userName }</h1>
</body>
...
```

#### 4. 결과

![alt](/assets/images/post/spring/27.png)

### 4) @Autowired

- **스프링 DI(Dependency Injection)**에서 사용되는 특별한 어노테이션임
- 의존하는 객체를 자동으로 주입해주는 어노테이션
- 기존 XML 파일에서 각각의 빈을 DI로 주입했던 기능을 코드에서 애너테이션으로 자동으로 수행함
- 별도의 setter나 생성자 없이 속성에 빈을 주입할수 있음.

### 5) @PathVariable

- 파라미터를 URL형식으로 받을 수 있도록 해줌
- 브라우저에서 요청 URL로 전달된 매개변수를 가져올 수 있음.
- ex)

```java
// 브라우저에서 요청시 {num} 부분의 값이 @PathVariable로 지정됨
	@RequestMapping(value="/notice/{num}")
	public int notice(@PathVariable("num") int num) throws Exception{
					// 요청 URL에서 지정된 값이 num에 자동으로 할당 됨
		return num;
	}
```

### 6) @RequestBody

- HttpRequestBody를 Java객체로 전달 받을 수 있음.
- 브라우저에서 전달되는 JSON 데이터를 객체로 자동 변환 해줌

### 7) @ResponseBody

- Java객체를 HttpResponseBody로 전송 할수 있음.
- jsp가 아닌 텍스트나 JSON으로 결과를 전송할 수 있음.

```java
@RequestMapping(value = "/res1")
	@ResponseBody			// 데이터 전송하도록 설정
	public Map<String, Object> res1() {	//Map 데이터를 브라우저로 전송함
		Map<String, Object> map = new HashMap<>();
		map.put("id", "bob");
		map.put("name", "이젠");

		return map;
	}
```

![alt](/assets/images/post/spring/35.png)

### 8) @ResponseEnitiy

- 답변시 데이터를 전달시 예외에 대해 세밀한 제어가 필요한 경우 사용함

```java
@RequestMapping("/membersList2")
	public ResponseEntity<List<MemberDTO>> listMembers2() {

		List<MemberDTO> list = new ArrayList<>();

		for (int i = 0; i < 10; i++) {
			MemberDTO dto = new MemberDTO();
			dto.setId("BOB" + i);
			dto.setPwd("0824" + i);
			dto.setName("정원영" + i);
			dto.setEmail("nicednjsdud" + i + "@gmail.com");
			list.add(dto);
		}
		// 오류코드 500으로 설정해서 응답함
		return new ResponseEntity<>(list,HttpStatus.INTERNAL_SERVER_ERROR);
	}
```

![alt](/assets/images/post/spring/36.png)

## 8. Model 클래스 이용해 값 전달

- 따로 뷰 정보를 전달할 필요가 없을 때 사용하면 편리함.

### loginController method 생성

- 입력값과 상관없이 BOB , 정원영이 result.jsp로 전달

```java
// 메서드 호출 시 Model 클래스 객체를 생성
	@RequestMapping(value ="/anno/login5.do",method = {RequestMethod.GET,RequestMethod.POST})
	public String login5(Model model ,HttpServletRequest request,HttpServletResponse response) throws IOException{
		request.setCharacterEncoding("UTF-8");
		model.addAttribute("userId","BOB");			// JSP에 전달할 데이터를 model에 바인딩
		model.addAttribute("userName","정원영");

		return "result";
	}
```
