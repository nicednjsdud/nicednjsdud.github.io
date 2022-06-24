---
title: JSP 20. 모델 mvc 게시판 수정/삭제 구현(5) 
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
last_modified_at: '2022-06-22 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델 2 (MVC) JSP board 구현 5
===========================

## 5. 수정 / 삭제

### 1) DAO 추가

* BoardDAO

```java
	// 입력한 비밀번호가 지정한 일련번호의 게시물의 비밀번호와 일치하는지 확인
	public boolean confirmPassword(String pass,String idx) {
		boolean isCorrect = true;
		
		String query = "SELECT count(*) FROM MVCBOARD WHERE pass = ? AND idx= ?";
		
		try {
			
// 비밀번호와 일련번호가 일치하는 게시물 개수를 세어 => 비밀번호 일치여부 확인
			psmt = conn.prepareStatement(query);
			psmt.setString(1, pass);
			psmt.setString(2, idx);
			rs =  psmt.executeQuery();			
			// 일치하는 게시물이 없다면 false
			rs.next();
			if(rs.getInt(1)==0) {
				isCorrect = false;
			}			
		} catch (SQLException e) {
			isCorrect=false;
			System.out.println("비밀번호 검증 중 예외 발생");
			e.printStackTrace();
		}	
		return isCorrect;
	}
	
	// 지정한 일련번호의 게시물 삭제
	
	public int deletePost(String idx) {
		int result = 0;
		
		String query = "DELETE FROM MVCBOARD WHERE idx= ?";
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, idx);			
			result = psmt.executeUpdate();	//정상적으로 삭제되었다면 1을 반환
			
			
		} catch (SQLException e) {
			System.out.println("게시물 삭제 중 예외 발생");
			e.printStackTrace();
		}
		
		return result;
		
	}

```

### 2) passController (수정 삭제 통합)

* passController.ava
* 비밀번호 검증

```java
package kr.co.ezenac.model2.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import kr.co.ezenac.model2.util.FileUtil;
import kr.co.ezenac.model2.util.JsFunction;

@WebServlet("/board/pass.do")
public class PassController extends HttpServlet {
	
	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse
	 response) throws ServletException, IOException {
		// mode 매개변수 값을 request 영역에 저장한다음 pass.jsp로 포워드 함.
		request.setAttribute("mode", request.getParameter("mode"));
		request.getRequestDispatcher("/board/pass.jsp").forward(request, response);
	}
	
	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse 
	response) throws ServletException, IOException {
		// 매개변수 저장
		String idx = request.getParameter("idx");
		String mode = request.getParameter("mode");
		String pass = request.getParameter("pass");
		
		BoardDAO dao = new BoardDAO();
		boolean confirmed = dao.confirmPassword(pass, idx);
		dao.close();
		
		if(confirmed) {			// 비밀번호 일치
			if(mode.equals("edit")) {		// 수정모드
				// 검증이 완료된 비밀번호를 session 영역에 저장
				HttpSession session = request.getSession();
				session.setAttribute("pass", pass);
				response.sendRedirect("../board/edit.do?idx="+idx);
			}
			else if(mode.equals("delete")) {	
				// 삭제모드 - 게시물이 첨부된 파일도 같이 삭제해야함
				dao = new BoardDAO();
				BoardDTO dto = dao.selectView(idx);	// 기존 정보를 보관 
				int result = dao.deletePost(idx);	// 게시물을 삭제
				dao.close();
				
				// 게시물 삭제 성공시 보관해둔 정보에서 파일이름을 찾아 첨부파일까지 삭제
				if(result == 1) {					
					String saveFileName = dto.getSfile();
					FileUtil.deleteFile(request, "/Uploads", saveFileName);
				}
				// 목록페이지로 이동
				JsFunction.alertLocation(response, "삭제되었습니다.", "../board/list.do");
			}
		}
		else {		// 비밀번호 불일치
			JsFunction.alertBack(response, "비밀번호 검증에 실패하였습니다.");
		}
		
	}
	
	
}

```

### 3) FileUtil 삭제기능 추가

```java
// 지정한 위치의 파일 삭제
	public static void deleteFile(HttpServletRequest request,String directory, String fileName) {
		// 파일이 저장된 디렉토리의 물리적 경로 얻어오기 
		String sDirectory = request.getServletContext().getRealPath(directory);
		// 경로와 파일명 결합하여 파일 객체 생성
		File file = new File(sDirectory+File.separator+fileName);
		
		// 경로의 파일이 존재하면 삭제
		if(file.exists()) {
			file.delete();
		}
	}
```

### 4) 수정 컨트롤러 생성

* EditController.java

```java
package kr.co.ezenac.model2.board;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.oreilly.servlet.MultipartRequest;

import kr.co.ezenac.model2.util.FileUtil;
import kr.co.ezenac.model2.util.JsFunction;

@WebServlet("/board/edit.do")
public class EditController extends HttpServlet {

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		String idx = request.getParameter("idx");	//수정할 게시물의 일련번호 받음
		
		BoardDAO dao = new BoardDAO();
		BoardDTO dto = dao.selectView(idx);			//기존 게시물을 내용을 담은 DTO 객체 얻음
		request.setAttribute("dto", dto);  			//request 영역에 저장(바인딩)
		
		request.getRequestDispatcher("/board/edit.jsp").forward(request, response);  // 포워딩
	}
	
	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//1. 파일 업로드 처리 -------------
		//업로드 시 디렉토리의 물리적 경로 확인
		String saveDirectory = request.getServletContext().getRealPath("/Uploads");
		
		//초기화 매개변수로 설정한 첨부 파일 최대 용량 확인 
		ServletContext application = getServletContext();
		int maxPostSize = Integer.parseInt(application.getInitParameter("maxPostSize"));
		
		//파일 업로드
		MultipartRequest mr = FileUtil.uploadFile(request, saveDirectory, maxPostSize);
		if(mr == null) {
			//파일 업로드 실패 - 경고창 띄워주고 작성 페이지로 다시 이동
			JsFunction.alertBack(response, "첨부 파일이 제한 용량을 초과합니다.");
			return;
		}
		
		//2.파일 업로드 외 처리
		//수정 내용을 매개변수로 얻어옴 
		String idx = mr.getParameter("idx");
		String prevOfile = mr.getParameter("prevOfile");
		String prevSfile = mr.getParameter("prevSfile");
		
		String name = mr.getParameter("name");
		String title = mr.getParameter("title");
		String content = mr.getParameter("content");
		
		HttpSession session =  request.getSession();
		String pass = (String) session.getAttribute("pass");
		
		BoardDTO dto = new BoardDTO();
		dto.setIdx(idx);
		dto.setName(name);
		dto.setTitle(title);
		dto.setContent(content);
		dto.setPass(pass);
		
		// 원본 파일명과 저장된 파일이름 설정
		String fileName = mr.getFilesystemName("ofile");
		
		if (fileName != null) {
			//첨부파일이 있을 경우 파일명 변경, 새로운 파일명 생성
			String now = new SimpleDateFormat("yyyyMMdd_HmsS").format(new Date());
			String ext = fileName.substring(fileName.lastIndexOf("."));		//파일 확장자
			String newFileName = now + ext;		// 새로운 파일 이름 ("업로드일시.확장자")
			
			//파일명 변경
			// File.separator : 경로 구분하는 특수 기호를 뜻함. OS에 따라 경로 표현 방법이 다름. 환경에 상관없이 코드 동작하게함.
			File oldFile = new File(saveDirectory + File.separator + fileName);
			File newFile = new File(saveDirectory + File.separator + newFileName);	
			oldFile.renameTo(newFile);		//파일이름 변경
			
			//dto에 저장
			dto.setOfile(fileName);			//원래 파일 이름
			dto.setSfile(newFileName);		//서버에 저장된 파일 이름			
			
			//기존파일 삭제
			FileUtil.deleteFile(request, "/Uploads", prevSfile);
		}
		else {
			//첨부 파일이 없는 경우 - 기존 이름 유지
			dto.setOfile(prevOfile);
			dto.setSfile(prevSfile);
		}
		
		//DB에 수정 내용 반영
		BoardDAO dao = new BoardDAO();
		int result = dao.updatePost(dto);
		
		//성공 or 실패
		if (result == 1) { 		//수정 성공
			session.removeAttribute("pass");
			response.sendRedirect("../board/view.do?idx=" + idx);
		}
		else {					//수정 실패
			JsFunction.alertLocation(response, "비밀번호 검증을 다시 진행해 주세요.", 
									"../board/view.do?idx=" + idx);
		}		
	}
}
```

### 5) 비밀번호 검증 페이지 생성

* pass.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>파일 첨부형 게시판 - 비밀번호 체크</title>
<script type="text/javascript">

	/* 비밀번호 입력했는지 확인 */

	function validateForm(form) {
		if(form.pass.value == ""){
			alert("비밀번호를 입력하세요")
			form.pass.focus()
			return false;
		}
	}
</script>
</head>
<body>
	<h2>파일 첨부형 게시판 - 비밀번호 검증</h2>
	<form action="../board/pass.do" name="writeFrm" method="post" onsubmit="return validateForm(this)">
	
	<!-- 삭제 혹은 수정할 게시물의 일련번호(idx)와 모드(mode)를 hidden 타입 입력상자에 저장함 -->
	<input type="hidden" name="idx" value="${param.idx }" />
	<input type="hidden" name="mode" value="${param.mode }" />
	<table border="1" width="90%">
		<tr>
			<td>비밀번호</td>
			<td>
				<input type="password" name="pass" style="width:100px;"/>		
			</td>
		</tr>
		<tr>
			<td colspan = "2" align="center">
				<button type="submit">비밀번호검증</button>
				<button type="reset">RESET</button>
				<button type="button" onclick="location.href='../board/list.do'">목록보기</button>
			</td>
		</tr>
	</table>
	</form>
</body>
</html>
```

![alt](/assets/images/post/jsp/164.png)


### 6) 수정페이지 생성

* edit.jsp

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
<title>파일 첨부형 게시판 - 수정 하기</title>
</head>
<body>
	<h2> 파일첨부형 게시판 - 수정하기 </h2>
	<form action="../board/edit.do" name="writeFrm" method="post"
		enctype="multipart/form-data" onsubmit="return validateForm(this)">
		
		<!-- hidden 타입 입력상자로 일련번호, 서버에 저장된 파일명, 원본 파일명 -->
		<input type="hidden" name="idx" value ="${dto.idx }" />
		<input type="hidden" name="prevOfile" value="${dto.ofile }" />
		<input type="hidden" name="prevSfile" vlaue="${dto.sfile }"/>
		<table border="1" width="90%">
			<tr>
				<td>작성자</td>
				<td><input type="text" name="name" style="width: 150px;" value="${dto.name }" /></td>
			</tr>
			<tr>
				<td>제목</td>
				<td><input type="text" name="title" style="width: 90%" value="${dto.title }" /></td>
			</tr>
			<tr>
				<td>내용</td>
				<td><textarea name="content" style="width: 90%; height: 100px;"  >${dto.content }</textarea>
				</td>
			</tr>
			<tr>
				<td>첨부파일</td>
				<td><input type="file" name="ofile"/></td>
			</tr>
			
			<tr>
				<td colspan="2" align="center">
					<button type="submit">작성 완료</button>
					<button type="reset">RESET</button>
					<button type="button" onclick="location.href='../board/list.do'">목록
						보기</button>
				</td>
			</tr>
		</table>
	</form>
</body>
</html>
```

![alt](/assets/images/post/jsp/165.png)
