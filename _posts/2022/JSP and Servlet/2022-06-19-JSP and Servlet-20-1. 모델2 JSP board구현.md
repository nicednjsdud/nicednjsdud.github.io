---
title: JSP 18. 모델 mvc 게시판 구현 DB생성/ 리스트 생성(2)
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
last_modified_at: '2022-06-19 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델 2 (MVC) JSP board 구현 2
===========================

## 1. 목록보기

### 1) DB

* 테이블 생성

![alt](/assets/images/post/jsp/138.png)

```sql
DROP TABLE mvcboard	CASCADE CONSTRAINTS;
CREATE TABLE mvcboard (
	idx	NUMBER PRIMARY KEY,
	name varchar2(50) NOT NULL,
	title varchar2(200) NOT NULL,
	content varchar2(2000) NOT NULL,
	postdate DATE DEFAULT sysdate NOT NULL,
	ofile varchar2(200),
	sfile varchar2(30),
	download NUMBER DEFAULT 0 NOT NULL,
	pass varchar2(50) NOT NULL,
	visitcount NUMBER DEFAULT 0 NOT null
);
```
* 시퀀스 객체 생성

```sql
-- 일련번호형 시퀀스(Sequence) 객체 생성
-- : 순차적으로 증가하는 순번을 반환하는 데이터베이스 객체임.
DROP SEQUENCE seq_board_num;
CREATE SEQUENCE seq_board_num
	INCREMENT BY 1				-- 1씩 증가
	START WITH 1				-- 시작값 1
	MINVALUE 1					-- 최소값 1
	nomaxvalue					-- 최대값은 무한대
	nocycle						-- 순환하지 않음
	nocache						-- 캐시 안함
	;
```

![alt](/assets/images/post/jsp/139.png)

* test 주입

```sql
INSERT INTO EZEN.MVCBOARD
(IDX, NAME, TITLE, CONTENT, PASS)
VALUES(seq_board_num.nextval, 'bob', 'bob의 개발일기', 
                '자바와 스프링을 공부하고있습니다.', '0824' );
```

![alt](/assets/images/post/jsp/140.png)

### 2) class 생성

* (통합) JDBConnection.java

```java
package kr.co.ezenac.model2common;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import javax.servlet.ServletContext;

public class JDBConnection {
	public Connection conn;
	public Statement stmt;
	public PreparedStatement psmt;
	public ResultSet rs;
	
	
		public JDBConnection(String driver, String url,String id, String pwd) {
			try {
				Class.forName(driver);
				conn = DriverManager.getConnection(url,id,pwd);
			} catch (ClassNotFoundException | SQLException e) {
				
				e.printStackTrace();
			}
		}
	public JDBConnection(ServletContext application) {
		// JDBC 드라이버 로드
		String driver = application.getInitParameter("OracleDriver");
		try {
			Class.forName(driver);

			// DB연결
			String url = application.getInitParameter("OracleURL");
			String id = application.getInitParameter("OracleId");
			String pwd = application.getInitParameter("OraclePw");
			conn = DriverManager.getConnection(url,id,pwd);
			System.out.println("db 연결 성공! - 매개변수 application");
		} catch (ClassNotFoundException | SQLException e) {
			e.printStackTrace();
		}
	}

	public void close() {
		try {
			if (rs != null)
				rs.close();
			if (stmt !=null)
				stmt.close();
			if (psmt != null)
				psmt.close();
			if (conn != null)
				conn.close();

		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
}

```

* 커넥션 풀 활용 context.xml

```xml
<!--
       name : 생성할 자원(풀) 이름 
       auth : 인증 주체
    	 type : 데이터 소스로 사용할 클래스 명 
    	 driverClassName : JDBC 드라이버의 클래스명
    	 url : 접속할 데이터베이스 주소와 포트 번호 및 SID
       maxActive : 동시에 최대로 DB에 연결할 수 있는 Connection
       maxWait : 새로운 연결이 생길 때까지 기다릴 수 있는 최대 시간
   	-->
     <Resource 
    	name="jdbc/oracle" 
    	auth="Conainer" 
    	type="javax.sql.DataSource" 
    	driverClassName="oracle.jdbc.driver.OracleDriver"
    	url="jdbc:oracle:thin:@localhost:1521:XE"
    	username="ezen"
    	password="0824"
    	maxTotal="50"
    	maxWaitMillis="-1"
    />  
```

* BoardDTO.java

```java
package kr.co.ezenac.model2.board;

import java.sql.Date;

public class BoardDTO {
	private String idx;
	private String name;
	private String content;
	private Date postdate;
	private String ofile;
	private String sfile;
	private int download;
	private String pass;
	private int visitcount;
	public String getIdx() {
		return idx;
	}
    // setter 생성
    //getter 생성
}
```

* BoardDAO.java

```java
package kr.co.ezenac.model2.board;

import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

import javax.servlet.ServletContext;

import kr.co.ezenac.model2common.JDBConnection;



public class BoardDAO extends JDBConnection {// DB 연결을 위한 클래스 상속
	
	public BoardDAO(ServletContext application) {	
		super(application);							
	}
	
	// (검색 조건에 맞게) 보드 테이블에 저장된 게시물의 개수 반환
	// 목록에서 번호를 출력
	public int selectCount(Map<String, Object> map) {
		int totalCount = 0;	// 결과(게시물 수)를 담는 변수
		
		// 게시물 수를 얻어오는 쿼리문
		// Map 컬렉션에 저장된 값(검색어)이 있는 경우 Map 컬렉션에 키로 저장된 
		//값이 있을때만 where절을 추가
		String query = "SELECT count(*) FROM mvcboard ";
		if(map.get("searchWord") !=null) {
			query += "WHERE "+map.get("searchField")+" "+" LIKE '%"
											+map.get("searchWord")+"%'";
		}
		
		 try {
			stmt = conn.createStatement();		
			// 쿼리문 실행하기 위해 Statement 객체 생성
			rs = stmt.executeQuery(query);		
			// SELECT 쿼리문 실행. 실행 결과는 Result객체에 담음
			rs.next();							
			// 커서를 첫번째 행으로 이동
			totalCount = rs.getInt(1);			
			// ResultSet객체의 1번(첫번째) 인덱스의 결과를 정수로 가져옴
		} catch (SQLException e) {
			e.printStackTrace();
		}
		
		
		return totalCount;
	}
	
	// board 테이블의 레코드를 가죠와서 반환함.
	// 이 메서드가 반환한 resultSet 객체로부터 게시물 목록을 반복하여 출력 (paging 기능)
	public List<BoardDTO> selectListPage(Map<String, Object> map){
		List<BoardDTO> board = new ArrayList<>(); // 게시물 목록(결과)을 담을 변수
		
		String query = "SELECT * FROM ( "+
					   "SELECT tb.*, ROWNUM rnum FROM ( "+
					   "SELECT * FROM MVCBOARD";
		if(map.get("searchWord") !=null) {	
			// Map컬렉션에 값이 있을때만 검색을 위한 where절 추가
			query += "WHERE "+map.get("searchField")+" "+" LIKE '%"
											+map.get("searchWord")+"%'";
		}
		query += " ORDER BY idx DESC"
				+ ") tb"
				+ ")"
				+ "where rNum BETWEEN ? AND ?";
		try {
			psmt = conn.prepareStatement(query);
			psmt.setString(1, map.get("start").toString());
			psmt.setString(1,map.get("end").toString());
			rs = psmt.executeQuery();
			
			while(rs.next()) {
				BoardDTO dto = new BoardDTO();
				
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
				
				board.add(dto);
				
			}
			
		} catch (SQLException e) {
			System.out.println("게시물 조회 중 예외 발생");
			e.printStackTrace();
			
		}
		
		return board;
	}
	
	
}
```

### 3) controller 작성 - 글 목록

* ListController

```java
package kr.co.ezenac.model2.board;

import java.io.IOException;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import kr.co.ezenac.model2.util.BoardPage;

public class ListController extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// DAO 생성
		BoardDAO dao = new BoardDAO();
		
		// 모델로 전달할 검색 매개변수 및 뷰로 전달할 페이징 관련 값을 저장하기 위해 Map 컬렉션 생성
		Map<String, Object> map = new HashMap<>();
		String searchField = request.getParameter("searchField");	// 검색어 폼값 받기
		String searchWord = request.getParameter("searchWord");

		if(searchWord !=null){		// 검색어가 있을때 Map에 저장
			map.put("searchField",searchField);
			map.put("searchWord",searchWord);
		}

		int totalCount = dao.selectCount(map);	//게시물 수 확인
		
		// 페이지 설정값 상수를 가져와서 페이지당 게시물수(pageSize)와 블록당 페이지수(blockPage)를 구함 
		ServletContext application = getServletContext();
		int pageSize = Integer.parseInt(application.getInitParameter("POSTS_PER_PAGE"));
		int blockPage = Integer.parseInt(application.getInitParameter("PAGE_PER_BLOCK"));
		
		// 현재 페이지 확인
		int pageNum = 1;			// default 값
		// 리턴타입이 문자열이므로 pageTemp에 임시저장
		String pageTemp = request.getParameter("pageNum");	
		if(pageTemp !=null && pageTemp.equals(""))
			pageNum =Integer.parseInt(pageTemp);	// 요청받은 페이지(정수)로 수정
		
		// 목록에 출력할 게시물 범위 계산
		int start = (pageNum - 1) * pageSize + 1;
		int end = pageNum * pageSize;
		
		map.put("start", start);
		map.put("end", end);
		
		// 게시물 목록 받기
		List<BoardDTO> boardLists = dao.selectListPage(map);
		dao.close(); //DC 연결 닫기
		
		// 뷰에 전달할 매개변수 추가
		
		String paingImag = BoardPage.pagingStr(totalCount, pageSize, blockPage, pageNum,"../board/list.do");
		
		map.put("paingImag", paingImag);
		map.put("totalCount", totalCount);
		map.put("pageSize", pageSize);
		map.put("pageNum", pageNum);
		
		// 전달할 데이터를 request 영역에 저장한 후 list.jsp로 포워드
		request.setAttribute("boardLists", boardLists);
		request.setAttribute("map", map);
		request.getRequestDispatcher("/board/list.jsp").forward(request, response);
	}
}
```

* list.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>파일 첨부형 게시판</title>
<style type="text/css">
	a{
		text-decoration: 
	}
</style>
</head>
<body>
	<h2>파일 첨부형 게시판 - 목록 보기(List)</h2>
	
	
	<form action="#" method="get">
		<table border="1" width="90%">
			<tr>
				<td align="center">
					<select name="searchField">
							<option value="title">제목</option>
							<option value="content">내용</option>
					</select> 
					<input type="text" name="searchWord" /> 
					<input type="submit" value="검색하기" />
				</td>
			</tr>
		</table>
		
		<!-- 게시물 목록 테이블 -->
		<table border="1" width=90%>
			<!-- 컬럼이름 -->
			<tr>
				<th width="10%">번호</th>
				<th width="40%">제목</th>
				<th width="15%">작성자</th>
				<th width="10%">조회수</th>
				<th width="15%">작성일</th>
				<th width="10%">첨부</th>
			</tr>
			<c:choose>
				<c:when test="${empty boardLists }" > <!-- 게시물이 없을 때 -->
				<tr>
					<td colspan="5" align="center">
						등록된 게시물이 없습니다.
					</td>
				</tr>
				</c:when>
				<c:otherwise>		<!-- 게시물이 있을 때 -->
					<c:forEach items="${boardLists }" var="row" varStatus="loop">
						<tr align="center">
							<td>	<!--  가상번호 -->
								<%-- 전체게시물수 - (((현재 페이지 번호 -1)* 페이지 사이즈)+varStaurs의 index값)
									17 - (((1-1) * 10 ) + 0) = 17
									17 - (((2-1) * 10 ) + 0) = 7
								 --%>
								 ${map.totalCount - (((map.pageNum-1)* map.pageSize)+loop.index)}
							</td>
							<td align="left">
								<a href="../board/view.do?idx=${row.idx }">${row.title }</a>
							</td>
							<td>${row.name }</td>
							<td>${row.visitcount }</td>
							<td>${row.postdate }</td>
							<td>
								<c:if test="${not empty row.ofile }">
									<a href="../board/download.do?ofile=${row.ofile }&sfile=${row.sfile}&idx=${row.idx}">[Down]</a>
								</c:if>
							</td>
						</tr>
					</c:forEach>
				</c:otherwise>
			</c:choose>
		</table>
			
			<!-- 하단메뉴 (페이징,글쓰기)  -->
		<table border="1" width="90%" >
				<tr align="center">
					<td>${map.pagingImag }</td>
					<td width="100">
						<button type="button" onclick="location.href='../board/write.do';">글쓰기</button>
					</td>
				</tr>
				
		</table>
	</form>
</body>
</html>
```

![alt](/assets/images/post/jsp/155.png)

### 4) 유틸추가

* JSFunction.java
* alert창을 위한 java 클래스

```java
package kr.co.ezenac.model2.util;

import java.io.PrintWriter;

import javax.servlet.http.HttpServletResponse;
import javax.servlet.jsp.JspWriter;

public class JsFunction {
	// 메세지 알림창을 띄우고 명시한 URL로 이동함.(ex. 로그인에 성공했습니다.
	public static void alertLocation(String msg, String url, JspWriter out) {
		try {
			String script = ""
							+"<script>"
							+"alert( '"+msg+"');"
							+"location.href='"+url+"'; "
							+"</script>";
			out.print(script);
		}catch(Exception e) {
			
		}
	}
	
	public static void alertLocation(HttpServletResponse response, String msg, String url) {
		try {
			response.setContentType("text/html;charset=UTF-8");
			PrintWriter out = response.getWriter();
			String script = ""
							+"<script>"
							+"alert( '"+msg+"');"
							+"location.href='"+url+"'; "
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
							+"alert( '"+msg+"');"
							+"history.back(); "
							+"</script>";
			out.print(script);
		}catch(Exception e) {
			
		}
	}
	
	public static void alertBack(HttpServletResponse response, String msg) {
		try {
			response.setContentType("text/html; charset=utf-8");
			PrintWriter out = response.getWriter();
			String script = ""
							+"<script>"
							+"alert( '"+msg+"');"
							+"history.back(); "
							+"</script>";
			out.print(script);
		}catch(Exception e) {
			
		}
	}
}

```













































