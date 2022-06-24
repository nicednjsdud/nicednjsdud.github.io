---
title: JSP 18. 모델 mvc 게시판 글쓰기 구현(3) 
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
last_modified_at: '2022-06-20 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델 2 (MVC) JSP board 구현 3
===========================

## 2. 글쓰기

### 1) 글쓰기 페이지 생성

* write.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script type="text/javascript">
	function validateForm(form) {		// 폼내용 검증
		if(form.name.value==""){
			alert("작성자를 입력하세요.")
			form.name.focus()
			return false
		}
		if(form.content.value==""){
			alert("내용을 입력하세요.")
			form.content.focus()
			return false
		}
		if(form.title.value==""){
			alert("제목을 입력하세요.")
			form.title.focus()
			return false
		}
		if(form.pass.value==""){
			alert("비밀번호를 입력하세요.")
			form.pass.focus()
			return false
		}
		
	}
	
</script>
<title>파일 첨부형 게시판</title>
</head>
<body>
	<form action="../board/write.do" name="writeFrm" method="post"
		enctype="multipart/form-data" onsubmit="return validateForm(this)">
		<table border="1" width="90%">
			<tr>
				<td>작성자</td>
				<td><input type="text" name="name" style="width: 150px;" /></td>
			</tr>
			<tr>
				<td>제목</td>
				<td><input type="text" name="title" style="width: 90%" /></td>
			</tr>
			<tr>
				<td>내용</td>
				<td><textarea name="content" style="width: 90%; height: 100px;"></textarea>
				</td>
			</tr>
			<tr>
				<td>첨부파일</td>
				<td><input type="file" name="ofile"/></td>
			</tr>
			<tr>
				<td>비밀번호</td>
				<td><input type="password" name="pass" style="width: 100px"/></td>
			</tr>
			<tr>
				<td colspan="2" align="center">
					<button type="submit">작성 완료</button>
					<button type="reset">다시 입력</button>
					<button type="button" onclick="location.href='../board/list.do'">목록
						보기</button>
				</td>
			</tr>
		</table>
	</form>
</body>
</html>
```

![alt](/assets/images/post/jsp/151.png)

### 2) DAO 추가

* BoardDAO.java

```java
// 게시글 데이터를 받아 DB에 추가함 (파일 업로드 지원)
	public int insertWrite(BoardDTO dto) {
		int result = 0;
		
		String query = "INSERT INTO MVCBOARD "+
						" (IDX, NAME, TITLE, CONTENT, OFILE, SFILE, PASS) "+
						" VALUES (seq_board_num.nextval, ?, ?, ?, ?, ?, ?)";
		
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, dto.getName());
			psmt.setString(2, dto.getTitle());
			psmt.setString(3, dto.getContent());
			psmt.setString(4, dto.getOfile());
			psmt.setString(5, dto.getSfile());
			psmt.setString(6, dto.getPass());
			
			result = psmt.executeUpdate();
			
		} catch (SQLException e) {
			System.out.println("게시물 입력 중 예외 발생");
			e.printStackTrace();
		}	
		return result;
	}
```

### 3) util 

* FileUtil.java

```java
package kr.co.ezenac.model2.util;

import java.io.IOException;

import javax.servlet.http.HttpServletRequest;

import com.oreilly.servlet.MultipartRequest;

public class FileUtil {
	
	// 파일 업로드(multipart/form-data 요청) 처리
	public static MultipartRequest uploadFile(HttpServletRequest request,
						String saveDirectory,int maxPostSize) {
		
		try {
			return new MultipartRequest(request, saveDirectory, 
												maxPostSize,"UTF-8" );
		} catch (IOException e) {
			e.printStackTrace();
			return null;
		}
		
	}
}

```

#### 3) Controller 생성

* WriteController.java

```java
package kr.co.ezenac.model2.board;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.oreilly.servlet.MultipartRequest;

import kr.co.ezenac.model2.util.FileUtil;
import kr.co.ezenac.model2.util.JsFunction;

public class WriteController extends HttpServlet {
	
	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// 글쓰기 폼으로 진입
		request.getRequestDispatcher("/board/write.jsp").forward(request, response);
	}
	
	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// 1. 파일 업로드 처리
		// 업로드 시 디렉토리 물리적 경로
		String saveDirectory = request.getServletContext().getRealPath("/Uploads");
		
		// (초기화 매개변수)첨부 파일 최대 용량 확인
		ServletContext application = getServletContext();
		// web.xml에 컨텍스트 초기화 매개변수로 설정해둔 업로드 제한 용량 얻어옴
		int maxPostSize = Integer.parseInt(application.getInitParameter("maxPostSize"));
		
		// 파일 업로드
		MultipartRequest mr = FileUtil.uploadFile(request, saveDirectory,maxPostSize );
		// 파일 업로드 실패시 경고창 띄어주고 작성 페이지 이동
		if(mr == null) {
			// 파일 업로드 실패 - 경고창 띄워주고 작성 페이지로 다시 이동
			JsFunction.alertLocation(response, "첨부 파일이 제한 용량을 초과합니다.","../board/write.do");
			return;
		}
		
		// 2. 파일 업로드 외 처리
		// form값을 dto에 저장
		BoardDTO dto = new BoardDTO();
		dto.setName(mr.getParameter("name"));
		dto.setTitle(mr.getParameter("title"));
		dto.setContent(mr.getParameter("content"));
		dto.setPass(mr.getParameter("pass"));
		
		// 원본 파일명
		String fileName = mr.getFilesystemName("ofile");
		if(fileName != null) {	// 첨부파일이 있을 때 파일명 변경
			 // 새로운 파일명 생성
	// yyyy - 년도 , MM - 월, dd - 일, H- 시간, m - 분, s- 초, S -밀리초
			String now = new SimpleDateFormat("yyyyMMdd_HmsS").format(new Date()); 
			String ext = fileName.substring(fileName.lastIndexOf(".")); // 파일 확장자
			String newFileName = now + ext;		// 새로운 파일 이름 ("업로드시.확장자")
			
			// 파일명 변경
			
			File oldfile = new File(saveDirectory + File.separator + fileName);
			File newfile = new File(saveDirectory + File.separator + newFileName);
			
			oldfile.renameTo(newfile);	// 파일이름 변경
			
			dto.setOfile(fileName);		// origin 파일 이름
			dto.setSfile(newFileName);	// 서버에 저장된 파일이름
		}
		
		BoardDAO dao = new BoardDAO();
		int result = dao.insertWrite(dto);
		
		dao.close();
		
		// 모든 작업이 오류없이 완료되었다면 목록으로 이동, 실패하면 글쓰기 페이지로 다시 돌아감
		if(result == 1)		// 글쓰기 성공
			response.sendRedirect("../board/list.do");
		else				// 글쓰기 실패
			response.sendRedirect("../board/write.do");
	}
}

```

![alt](/assets/images/post/jsp/152.png)

* list 

![alt](/assets/images/post/jsp/153.png)

* DB 

![alt](/assets/images/post/jsp/154.png)












































