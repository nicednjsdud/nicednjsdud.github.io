---
title: JSP 14. 모델 1 방식
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
last_modified_at: '2022-06-08 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

모델1방식
==========

## 1. 요약

* DB와 연동하여 data를 입력, 수정, 삭제, 조회할수 있는 모델 1방식 회원제  
  게시판 제작

### 1) 폼값 처리에는 내장 객체 사용
    * 로그인은 session 영역 사용

### 2) 목록 보기

* 글쓰기
* 상세보기
* 수정하기
* 삭제하기

## 2. 구상

### 1) 회원제 게시판 프로세스

```
        ---------------------------------------------------------
        |                                                       |
        |                                                       |
        \/                                                      |
    목록보기화면    ------------>    글쓰기 화면  ----------> 글쓰기 처리
    (list.jsp)      글쓰기 클릭     (write.jsp)         (wirteProcess.jsp)

        |
        |
        |
제목클릭\/
                 수정 클릭 
     상세보기화면 ------------> 수정하기 화면 --------->  수정 처리 
     (view.jsp)               (edit.jsp)   작성완료 클릭 (editProcess.jsp)
        |   /\                                             |
        |   |                                              |
        |   |-----------------------------------------------
        |
        \/
    삭제 처리           --> 목록보기 화면
    (deleteprocess.jsp)
```
### 2) 로그인 처리 프로세스

### 3) 글쓰기 처리 프로세스

![alt](/assets/images/post/jsp/100.png)

### 3) 상세보기 처리 프로세스 

![alt](/assets/images/post/jsp/101.png)

### 4) 수정하기 처리 프로세스

![alt](/assets/images/post/jsp/102.png)

## 3. 테이블 및 시퀀스 생성 

* 게시판은 작성한 게시물을 DB에 저장한 후 관리
* DB에는 회원정보 저장할 테이블, 게시물을 저장할 테이블 생성

### 1) 테이블 board

* 사용자가 입력한 게시물 저장
* 기본키로 사용되는 컬럼(num)
    * 시퀀스를 통해 부여되는 순번을 입력하게 됨
        * sequence : 순차적으로 증가하는 순번을 생성해 중복되지 않는 정수값  
          을 반환하는 DB 객체

![alt](/assets/images/post/jsp/94.png)

```sql
DROP TABLE board CASCADE CONSTRAINTS;
CREATE TABLE board (
		num NUMBER PRIMARY KEY ,
		title varchar2(200) NOT NULL,
		content varchar2(2000) NOT NULL,
		id varchar2(10) NOT NULL,
		postdate DATE DEFAULT sysdate NOT NULL,
		visitcount number(6)
);
-- 외래키로 테이블 사이의 관계 설정
-- board 테이블의 id 컬럼이 member 테이블의 id컬럼을 참조하도록 
-- 해주는 외래키 생성
ALTER TABLE board ADD CONSTRAINT board_member_fk FOREIGN KEY (id) 
REFERENCES member(id);
```

![alt](/assets/images/post/jsp/95.png)

### 2) 시퀀스 객체 생성

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

### 3) 객체 insert

```sql
INSERT INTO board VALUES (seq_board_num.nextval, 
                '오늘은 6월 2째주','월요일같은 화요일입니다.'
		        ,'EZEN',sysdate,0);
COMMIT;
```

![alt](/assets/images/post/jsp/96.png)

### 4) web.xml에 DB접속 정보 추가

```xml
    ...
  <!-- 오라클 DB 접속 정보 : 초기화 매개변수로 입력 -->
  <context-param>
  	<param-name>OracleDriver</param-name>
  	<param-value>oracle.jdbc.driver.OracleDriver</param-value>
  </context-param>
  <context-param>
  	<param-name>OracleURL</param-name>
  	<param-value>jdbc:oracle:thin:@localhost:1521:XE</param-value>
  </context-param>
  <context-param>
  	<param-name>OracleId</param-name>
  	<param-value>ezen</param-value>
  </context-param>
  <context-param>
  	<param-name>OraclePw</param-name>
  	<param-value>0824</param-value>
  </context-param>
</web-app>
```

### 5) JDBConnection.java 생성

```java
package kr.co.ezenac.model1.common;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class JDBConnection {
	public Connection conn;
	public PreparedStatement psmt;
	public ResultSet rs;
	
	public JDBConnection(ServletContext application) {
		// JDBC 드라이버 로드
		String driver = application.getInitParameter("OracleDriver");
		try {
			Class.forName(driver);

			// DB연결
			String url = application.getInitParameter("OracleURL");
			String id = application.getInitParameter("OracleId");
			String pwd = application.getInitParameter("OralcePwd");
			conn = DriverManager.getConnection(url,id,pwd);
			System.out.println("db 연결 성공! - 매개변수 생성자");
		} catch (ClassNotFoundException | SQLException e) {
			e.printStackTrace();
		}
	}

	public void close() {
		try {
		if(rs !=null) rs.close();
		if(psmt !=null) rs.close();
		if(conn !=null) rs.close();
		
		} catch(SQLException e) {
			e.printStackTrace();
		}
	}
}
```

### 6) BoardDTO.java 생성

```java
package kr.co.ezenac.model1.board.dto;

import java.sql.Date;

public class BoardDTO {
	// 멤버 변수
	private String num;
	private String title;
	private String content;
	private String id;
	private Date postdate;
	private String visitcount;
	private String name;
	
    // 생성자
    public BoardDTO() {}
	// 게터/세터
	public String getNum() {return num;}
	public void setNum(String num) {this.num = num;}
	public String getTitle() {return title;}
	public void setTitle(String title) {this.title = title;}
	public String getContent() {return content;}
	public void setContent(String content) {this.content = content;}
	public String getId() {return id;}
	public void setId(String id) {this.id = id;}
	public Date getPostdate() {return postdate;}
	public void setPostdate(Date postdate) {this.postdate = postdate;}
    public String getVisitcount() {return visitcount;}
	public void setVisitcount(String visitcount) {
        this.visitcount = visitcount;}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}	
}
```












## 4. 모델1 구조와 모델 2 구조 (MVC 패턴)

### 1) MVC 패턴

![alt](/assets/images/post/jsp/97.png)

* 웹 어플리케이션은 사용자의 요청을 받아 처리한 후 응답하는 구조
* Model, View, Controller
    * 데이터 처리를 담당하는 모델
    * 화면 출력을 담당하는 뷰
    * 이 둘을 제어하는 컨트롤러

* 소프트웨어 개발 방법론의 일종



### 2) 모델1 방식

![alt](/assets/images/post/jsp/98.png)

* 개발 속도 빠름
* 배우기 쉬움
* 코드가 복잡해지고 유지보수가 어려움

### 3) 모델2 방식

![alt](/assets/images/post/jsp/99.png)

* 모델, 뷰, 컨트롤러가 각자의 역할 수행
* 업무 분담 명확해지고 코드가 간결해짐 => 유지보수도 쉬워짐
* 개발기간이 길어질수 있으므로 작은 프로젝트에는 부적합함.