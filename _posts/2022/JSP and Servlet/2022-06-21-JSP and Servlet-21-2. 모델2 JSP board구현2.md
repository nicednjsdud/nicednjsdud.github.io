---
title: JSP 19. 모델 mvc 게시판 상세보기/ 다운로드 구현(4) 
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
last_modified_at: '2022-06-21 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델 2 (MVC) JSP board 구현 4
===========================

## 3. 상세보기

### 1) DAO 메서드 추가

* BoardDAO.java

```java
// 주어진 일련번호에 해당하는 게시물을 DTO에 담아 반환
	public BoardDTO selectView(String idx) {
		BoardDTO dto = new BoardDTO();
		
		String query = "SELECT * FROM MVCBOARD WHERE IDX = ?";
		
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, idx);
			rs = psmt.executeQuery();	// 쿼리문 실행
			
			if(rs.next()) {
				dto.setIdx(rs.getString(1));
				dto.setName(rs.getString(2));
				dto.setTitle(rs.getString(3));
				dto.setContent(rs.getString(4));
				dto.setPostdate(rs.getDate(5));
				dto.setOfile(rs.getString(6));
				dto.setSfile(rs.getString(7));
				dto.setDownload(rs.getInt(8));
				dto.setPass(rs.getString(9));
				dto.setVisitcount(rs.getInt(10));
			}
			
		} catch (SQLException e) {
			System.out.println("게시물 상세보기 중 예외 발생");
			e.printStackTrace();
		}
		
		
		return dto;			// 결과 반환
		
	}
	
	// 주어진 일련변호에 해당하는 게시물의 조회수를 1 증가시킴
	public void updateVisitCount(String idx) {
		
		String query = "UPDATE MVCBOARD SET VISITCOUNT = VISITCOUNT +1 "+
						" WHERE idx= ?";
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, idx);
			psmt.executeQuery();
			
		} catch (SQLException e) {
			System.out.println("게시물 조회수 증가 중 예외 발생");
			e.printStackTrace();
		}
	}
```

### 2) controller 생성

* ViewController.java

```java
package kr.co.ezenac.model2.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/board/view.do")
public class ViewController extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, 
			HttpServletResponse response) throws ServletException, IOException {
		
		BoardDAO dao = new BoardDAO();
		String idx = request.getParameter("idx");
		
		dao.updateVisitCount(idx); 	// 조회수 1 증가
		BoardDTO dto = dao.selectView(idx);
		dao.close();
		
// 게시물 내용 줄바꿈 처리- HTML문서는 일반 텍스트 문서의 줄바꿈 문자(\r\n)를 
// 무시하기 때문에. HTML이 인식하는 줄바꿈 태그(<br>)로 바꿔줌
		dto.setContent(dto.getContent().replaceAll("\r\n", "<br>"));
		// 게시물 저장(바인딩) 후 뷰로 포워딩
		request.setAttribute("dto", dto);
		request.getRequestDispatcher("/board/view.jsp").forward(request, response);
		
	}
}

```

### 3) view 생성

* view.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>상세 보기</title>
</head>
<body>
	<h2>파일 첨부형 게시판 - 상세 보기(View)</h2>
	<table border="1" width="90%">
		<colgroup>
			<col width="15%" />
			<col width="35%" />
			<col width="15%" />
			<col width="*" />
		</colgroup>
		<!-- 게시글 내용 -->
		<tr>
			<td>번호</td><td>${dto.idx }</td>
			<td>작성자</td><td>${dto.name }</td>
		</tr>
		<tr>
			<td>작성일</td><td>${dto.postdate }</td>
			<td>조회수</td><td>${dto.visitcount }</td>
		</tr>
		<tr>
			<td>제목</td>
			<td colspan="3">${dto.title }</td>
		</tr>
		<tr>
			<td>내용</td>
			<td colspan="3" height="100">${dto.content }</td>
		</tr>
		
		<!-- 첨부파일 -->
		<tr>
			<td>첨부파일</td>
			<td>
				<c:if test="${not empty dto.ofile}">
					${dto.ofile }
					<a href="../board/download.do?ofile=${dto.ofile }&sfile=${dto.sfile}&idx=${dto.idx}">[다운로드]</a>	
				</c:if>
			</td>
			<td>다운로드수</td>
			<td>${dto.download }</td>
		</tr>	
		<tr>
			<td colspan="4" align="center">
				
				<button type="button" onclick="location.href='../board/pass.do?mode=edit&idx=${param.idx}'" >
					수정
				</button>
				<button type="button" onclick="location.href='../board/pass.do?mode=delete&idx=${param.idx}'" >
					삭제
				</button>
				<button type="button" onclick="location.href='../board/list.do'" >
					목록보기
				</button>
			</td>
		</tr>
	</table>
</body>
</html>
```

![alt](/assets/images/post/jsp/156.png)

## 4. 다운로드 

### 1) FileUtil 메서드 추가

* FileUtil.java

```java
// 파일을 다운로드 
	public static void download(HttpServletRequest request,HttpServletResponse response,
				String directory, String sfileName, String ofileName) {
		
		try {
		// 업로드 폴더의 물리적 경로 얻어오기
		String sDirectory = request.getServletContext().getRealPath(directory);
		
		//파일을 찾아 입력스트림 생성
		File file = new File(sDirectory, sfileName);
		InputStream inStream = new FileInputStream(file);
		
		// 한글파일명 깨짐 방지
		String client =  request.getHeader("User-Agent");
		
		// 인터넷 익스플로러가 아닌 경우
		if(client.indexOf("WOW64") == -1){
			
			// 원본 파일명을 getBytes("utf-8")로 바이트 배열로 변환후, iso-8859-1 캐릭터 셋 문자열로 재생성함
			ofileName = new String(ofileName.getBytes("utf-8"),"iso-8859-1");
		}
		else{
			ofileName = new String(ofileName.getBytes("KSC5601"),"iso-8859-1");
		}
		
		// 파일을 다운로드하기 위한 응답 헤더 설정
		response.reset();		// 응답 헤더 초기화
		
		// 파일 다운로드 창을 띄우기 위한 컨텐츠 타입 지정 (oct-stream : 8 비트 단위의 바이너리 데이터를 의미함)
		response.setContentType("application/octet-stream");
		
		// 웹 브라우저에서 파일 다운로드 창이 뜰때 원본 파일명이 기본으로 입력되어 있도록 설정
		response.setHeader("Content-Disposition", "attachment; filename= \""+ofileName+"\"");
		response.setHeader("Content-Length", ""+file.length());
		
		// 출력스트림 초기화
//		out.clear();
//		out = pageContext.pushBody();	
		// response로부터 새로운 출력 스트림 생성
		OutputStream outputStream = response.getOutputStream();
		
		// 출력 스트림에 파일 크기 배열 이용해서 파일 내용 출력
		byte[] b = new byte[(int)file.length()];
		int readBuffer = 0;
		
		while((readBuffer = inStream.read(b))>0){
			outputStream.write(b,0,readBuffer);
		}
		
		inStream.close();
		outputStream.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
```

### 2) DAO 다운로드 증가수 메서드 추가

* boardDAO.java

```java
    // 다운로드 횟수 1 증가
	public void downCountPlus(String idx) {
		
		String query = "UPDATE MVCBOARD SET DOWNLOAD = DOWNLOAD +1 "+
				" WHERE idx= ?";
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, idx);
			psmt.executeQuery();
			
		} catch (SQLException e) {
			System.out.println("다운로드 수 증가 중 예외 발생");
			e.printStackTrace();
		}
	}
```

### 3) DownloadController 생성

* DownloadController.java

```java
package kr.co.ezenac.model2.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import kr.co.ezenac.model2.util.FileUtil;

@WebServlet("/board/download.do")
public class DownloadController extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
												throws ServletException, IOException {
		
		// 매개변수 받기
		String ofile = request.getParameter("ofile");// 원본파일영
		String sfile = request.getParameter("sfile");// 저장된 파일명
		String idx =  request.getParameter("idx");	// 게시물 일련번호
		
		// 파일 다운로드
		FileUtil.download(request, response, "/Uploads", sfile, ofile);
		
		// 해당 게시물의 다운로드 수 1 증가
		BoardDAO dao = new BoardDAO();
		dao.downCountPlus(idx);
		dao.close();
	}
}

```

![alt](/assets/images/post/jsp/158.png)
![alt](/assets/images/post/jsp/159.png)
