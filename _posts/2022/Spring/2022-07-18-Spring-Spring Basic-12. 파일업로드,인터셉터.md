---
title: (Spring) 12. 파일 업로드 구현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: 파일 업로드 구현
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-18 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# File Upload 구현 (Spring)

## 1. 다중 파일 업로드

- **CommonsMultipartResolver** 클래스를 이용하면 여러개 파일 한꺼번에 업로드 가능

## 2. 스프링 인터셉터 (intercepter)

- 브라우저 요청 시 요청 메서드 호출 전후에 개발자가 원하는 기능을 수행함
- 필터와 기능이 유사하지만 필터보다 좀더 자유롭게 위치를 변경해서 기능을 수행함
- 쿠키 제어, 파일 업로드 등의 작업을 수행함

## 3. Test

### 1) pox.xml에 라이브러리 추가

```xml
<!-- 다중파일 업로드 -->
		<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
		<dependency>
			<groupId>commons-fileupload</groupId>
			<artifactId>commons-fileupload</artifactId>
			<version>1.4</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
		<dependency>
			<groupId>commons-io</groupId>
			<artifactId>commons-io</artifactId>
			<version>2.7</version>
		</dependency>
```

### 2) servlet - context 설정

- CommonsMultipartResolver클래스를 사용하기위해서는 몇가지 설정이 더필요하다.

```xml
	<!-- MultipartResolver -->
	<beans:bean id="multipartResolver"
		class="org.springframework.web.multipart.commons.CommonsMultipartResolver">

		<!-- 최대로 업로드가 가능한 파일의 크기 설정 -->
		<beans:property name="maxUploadSize" value="50000000" />

		<!-- 디스크에 임시 파일을 생성하기 전 메모리 보관할수 있는 최대 바이트 크기 설정 -->
		<beans:property name="maxInMemorySize" value="1000000" />

		<!-- 전달되는 매개변수의 인코딩 -->
		<beans:property name="defaultEncoding" value="utf-8" />
	</beans:bean>
```

### 3) 입력받을 폼 생성

- uploadForm.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%> <%@ taglib prefix="c"
uri="http://java.sun.com/jsp/jstl/core" %>
<c:set var="contextPath" value="${pageContext.request.contextPath}" />

<% request.setCharacterEncoding("UTF-8"); %>

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>파일 업로드 하기</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script type="text/javascript">
      let cnt = 1;
      //파일추가 클릭하면 동적으로 파일 업로드를 추가함
      //name 속성값으로 file+cnt를 설정함으로서 값을 다르게 해줌
      function fnAddFile() {
        $("#d_file").append(
          "<br />" + "<input type='file' name='file" + cnt + "'/>"
        );
        cnt++;
      }
    </script>
  </head>
  <body>
    <h1>파일 업로드 하기</h1>
    <form
      action="${contextPath}/upload"
      method="post"
      enctype="multipart/form-data"
    >
      <label>아이디 : </label>
      <input type="text" name="id" /><br />
      <label>이름 : </label>
      <input type="text" name="name" /><br />
      <input type="button" value="파일 추가" onclick="fnAddFile()" /><br />

      <!-- 파일 추가 클릭하면 동적으로 파일 업로드를 추가함 -->
      <div id="d_file"></div>

      <input type="submit" value="업로드" />
    </form>
  </body>
</html>
```

![alt](/assets/images/post/spring/31.png)

### 4) 입력받은 파일 처리할 컨트롤러 생성

- FileUploadController.java를 생성해 따로생성한 폴더안에 입력받는다.

```java
package kr.co.fileinter.fileupdown;

import java.io.File;
import java.util.ArrayList;
import java.util.Enumeration;
import java.util.HashMap;
import java.util.Iterator;
import java.util.List;
import java.util.Map;

import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.multipart.MultipartFile;
import org.springframework.web.multipart.MultipartHttpServletRequest;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class FileUploadController {

	//파일 저장 위치 지정
	private static final String CURR_IMAGE_PEPO_PATH =
        "/Users/jeong-won-yeong/Documents/Spring/workspace-spring/imageRepo";

	@RequestMapping(value = "/form")
	public String form() {
		return "uploadForm";		//업로드창인 uploadForm.jsp를 반환함
	}

	@RequestMapping(value = "/upload" , method = RequestMethod.POST)
	public ModelAndView upload(MultipartHttpServletRequest multipartRequest,
                                            HttpServletResponse response)
			throws Exception {
		multipartRequest.setCharacterEncoding("utf-8");

		//매개변수 정보와 파일 정보를 저장할 Map을 생성함
		Map map = new HashMap();
		Enumeration enu = multipartRequest.getParameterNames();

		//전송된 매개변수 값을 key/value로 map에 저장함
		while(enu.hasMoreElements()) {
			String name = (String) enu.nextElement();
			String value = multipartRequest.getParameter(name);
			map.put(name, value);
		}


		//파일을 업로드한 후 반환된 파일이름이 저장된 fileList를 다시 map 저장함
		List<String> fileList = fileProcess(multipartRequest);
		map.put("fileList", fileList);

		//map을 결과창으로 포워딩함
		ModelAndView mav = new ModelAndView();
		mav.addObject("map", map);
		mav.setViewName("result");

		return mav;
	}

	//첨부한 파일 이름이 저장된 fileList 리턴함
	private List<String> fileProcess(MultipartHttpServletRequest multipartRequest)
                                                            throws Exception {
		List<String> fileList = new ArrayList<>();

		//첨부된 파일 이름 가져옴
		Iterator<String> fileNames = multipartRequest.getFileNames();
		while(fileNames.hasNext()) {
			String fileName = fileNames.next();
			//파일 이름에 대한 MultipartFile 객체를 가져옴
			MultipartFile mFile = multipartRequest.getFile(fileName);
			String originalFilename =  mFile.getOriginalFilename();			//실제 파일 이름 가져옴

			fileList.add(originalFilename);									//파일 이름을 하나씩 fileList에 저장

			File file = new File(CURR_IMAGE_PEPO_PATH +"\\"+ fileName);
			if(mFile.getSize() != 0) {										//첨부된 파일이 있는지 체크
				if(!file.exists()) {										//경로에 파일이 없으면 그 경로에 해당하는
					if(file.getParentFile().mkdirs()) {						//디렉토리를 만든 후 파일을 생성함
						file.createNewFile();
					}
				}
				//임시로 저장된 MultipartFile을  실제 파일로 전송
				mFile.transferTo(new File(CURR_IMAGE_PEPO_PATH +"\\"+ originalFilename));
			}
		}
		return fileList;			//첨부한 파일 이름이 저장된 fileList 반환함
	}

}
```

- 다운로드 받은 파일을 화면에 뿌릴수 있는 컨트롤러 생성 (목적상)
- FileDownloadController.java

```java
package kr.co.fileinter.fileupdown;

import java.io.File;
import java.io.FileInputStream;
import java.io.OutputStream;

import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class FileDownloadController {
	// 파일 저장 위치 지정
	private static final String CURR_IMAGE_PEPO_PATH = "/Users/jeong-won-yeong/Documents/Spring/workspace-spring/imageRepo";

	@RequestMapping("/download") // 다운로드할 이미지 파일 이름을 전달함
	public void download(@RequestParam("imageFileName") String imageFileName, HttpServletResponse response)
			throws Exception {

		OutputStream out = response.getOutputStream();

		String downFile = CURR_IMAGE_PEPO_PATH + "\\" + imageFileName;
		// 다운로드될 파일 객체 생성
		File file = new File(downFile);

		response.setHeader("Cache-Control", "no-cache");
		// 헤더에 파일이름 설정
		response.addHeader("Content-disposition", "attachment; fileName=" + imageFileName);

		FileInputStream in = new FileInputStream(file);
		byte[] buffer = new byte[1024 * 8]; // 버퍼를 이용해 한꺼번에 8kbyte씩 브라우저에 전송됨
		while (true) {
			int count = in.read(buffer);
			if (count == -1)
				break;
			out.write(buffer, 0, count);
		}
		in.close();
		out.close();
	}
}

```

### 5) 결과를 뿌릴 jsp 생성

- result.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<c:set var="contextPath" value="${pageContext.request.contextPath}" />

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>결과</title>
</head>
<body>
	<h1>업로드가 완료되었습니다.</h1>
	<label>아이디 : </label>
	<input type="text" name="id" value="${map.id }" readonly /><br/>
    <!-- map으로 넘어온 매개변수 값을 표시 -->
	<label>이름 : </label>
	<input type="text" name="name" value="${map.name }" readonly /><br/>
    <!-- map으로 넘어온 매개변수 값을 표시 -->

	<div>
		<!-- 업로드한 파일들 forEach문 이용해 img 태그에 표시함 -->
		<c:forEach var="imageFileName" items="${map.fileList }">
			<img alt="이미지" src="${contextPath}/download?imageFileName=${imageFileName}">
			<br/><br/><br/>
		</c:forEach>
	</div>
</body>
</html>
```

![alt](/assets/images/post/spring/32.png)
