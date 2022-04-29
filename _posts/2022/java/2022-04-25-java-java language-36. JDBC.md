---
title: Java 32. JDBC
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: JDBC
tag : java language
article_tag1: java IO
article_section: java IO
meta_keywords: java,java languagem, JDBC
last_modified_at: '2022-04-25 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JDBC
=====

## 데이터베이스 연동 자바 프로그래밍

![alt](/assets/images/post/java/1.png)


### 1. 데이터베이스 접속 자바 클래스

```java
   -  Class.forName("클래스이름"); <-- JDbC 드라이버를 로딩
```

### 2. Connection 객체 생성

```java
   - DriverManager.getConnection (String url,String user, String password);
```

### 3. Statement 객체 생성 - SQL문을 실행

```java
   - Connection 객체의 createStatement();
```

### 4. Statement 객체의 executeQuery(String sql)
* 실행해서 ResultSet 객체를 생성
* executeUpdate(String sql) **둘중 하나 생성**

### 5. ResultSet 결과 테이블에서 커서가 투플을 가리킴

```java
    - next() : 다음 투플을 가리킴
    - getInt(int columnIndex) : columnIndex가 가리키는 열 값을 정수로 반환
```

### 실습 

#### 1. 테이블 생성

```sql
CREATE TABLE book (
	bookId NUMBER (2)	NOT NULL	PRIMARY KEY,
	bookname varchar2(40),
	publisher varchar2(40),
	price number(8)
);

INSERT INTO book VALUES (1, '축구의 역사','굿스포츠', 7000);
INSERT INTO book VALUES (2, '축구아는 여자','나무수', 13000);
COMMIT;
```

![alt](/assets/images/post/java/2.png)

#### 2. 연결

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class BookListTest {
	// 데이터베이스와 연결을 담당
	Connection conn;
	
	public BookListTest() {	// 생성자 초기화
		String url = "jdbc:oracle:thin:@localhost:1521:xe";
		String userid = "ezen";
		String pwd = "0824";
		
		try {
			// 드라이버 찾는 과정
			Class.forName("oracle.jdbc.driver.OracleDriver"); // 1번
			System.out.println("드라이버 로드 성공");
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}	
		
		try {
			System.out.println("데이터베이스 연결 준비...");
			conn = DriverManager.getConnection(url, userid, pwd);	  // 2번
			System.out.println("데이터베이스 연결 성공");
		} catch (SQLException e) {
			e.printStackTrace();
		}		
	}
	
	public static void main(String[] args) {
		BookListTest bookListTest = new BookListTest();
		bookListTest.sqlRun();	// 3번
	}


	public void sqlRun() { 
		// sql문
		String query = "select * from Book";
		try {
			// 인파라미터가 없는 정적 쿼리문을 실행할 때 사용됨
			// PreparedStatement - 파라미터가 있는 동적 쿼리문 실행할 떄 사용됨.
			Statement stmt = conn.createStatement();
			
			// select 쿼리문의 결과를 저장할 때 사용됨.
			ResultSet rs = stmt.executeQuery(query); //4번
			System.out.println("BOOk no \tBOOK NAME \t\tPUBLISHER \t PRICE ");
			while(rs.next()) { // 5번
				System.out.print("\t"+rs.getInt(1));
				System.out.print("\t"+rs.getString(2));
				System.out.print("\t\t"+rs.getString(3));
				System.out.print("\t\t"+rs.getInt(4));
				System.out.println();
			}
			
			conn.close();
			
			
		} catch (SQLException e) {
			e.printStackTrace();
		}
		
	}

}
```

![alt](/assets/images/post/java/3.png)
