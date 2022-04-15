---
title: Java 26. 예외처리 (Exception)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: about Exception
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, exception
last_modified_at: '2022-04-13 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---
예외처리
=========
## 프로그램에서의 오류
### 1. 컴파일 오류(compile error)
    - 프로그램 코드 작성 중 발생하는 문법적 오류 => detection 됨
### 2. 실행 오류 (rumtime error)
    - 실행 중인 프로그램이 의도하지 않는 동작(bug)을 하거나 
      프로그램이 중지 되는 오류
    - 실행 오류는 비정상 종료가 되는 경우 시스템의 심각한 장애를 발생할 수 있음.

* 자바 예외 처리를 통하여 프로그램의 비정상 종료 막고 log를 남길 수 있음.  
    - 시스템이 원활이 실행되도록 함.

## 예외(Exception)
### 1. 프로그램에서 제어 할 수 있는 오류
    - 읽으려는 파일이 없는 경우
    - 네트웍이나 소켓 연결 오류 등 자바 프로그램에서는 예외에 대한 처리를 수행 함.

	- 자바는 안정성이 중요한 언어로 대부분 프로그램에서 발생하는 오류에 대해 문법적으로 
      예외처리를 해야함.

### 2. 예외 클래스들
 * 최상 클래스 Exception
   - IOException : (입출력 예외 처리) 
   - RuntimeException (실행 오류 예외 처리) 

```
- ArithmeticException :  정수를 0으로 나눈 경우 발생
- NullPointerException : 초기화 되지 않은 Object를 사용하는 경우
- ArrayIndexOutOfBoundsException : 배열의 크기를 넘어서 위치를 참조하는 경우 
- FileNotFoundException : 참조하는 파일이 지정된 위치에 존재하지 않는 경우
```

```java
public class ArrayExceptionTest {

	public static void main(String[] args) {
		int arr[]=new int [5];
		for(int i=0;i<=5;i++) {			// Err 실제로 6개
			System.out.println(arr[i]);
		}
	}

}
```
    //Err 
    java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5         

## 예외 처리하기와 미루기
### 1. try ~ catch 문
    try{

        예외가 발생할 수 있는 코드 부분

    }catch(처리할 예외타입 e){

        try 블록 안에서 예외가 발생했을 때 
        예외를 처리하는 부분
    }

```java
public class ArrayExceptionTest {

	public static void main(String[] args) {
		int arr[]=new int [5];
		try {
			for(int i=0;i<=5;i++) {			
				System.out.println(arr[i]);
			}
		}catch(ArrayIndexOutOfBoundsException e) {
			System.out.println(e);
			System.out.println("예외 처리");
		}
		System.out.println("프로그램 종료");
	}

}
```
### 2. try ~ catch ~ finally 문
    try{

        예외가 발생할 수 있는 코드 부분

    }catch(처리할 예외타입 e){

        try 블록 안에서 예외가 발생했을 때 
        예외를 처리하는 부분

    }finally{

        예외 발생 여부와 상관 없이 항상 수행되는 부분
        리소스를 정리하는 코드를 주로 씀
    }

* finally 블럭에서 파일을 닫거나 네트웤을 닫는 등의 리소스 해체 구현을 함.

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileExceptionHanding {

	public static void main(String[] args) {
		FileInputStream fis = null;
		try {
			fis =new FileInputStream("Hello.txt");
		} catch (FileNotFoundException e) {
			System.out.println(e);
			
		} finally {
			if(fis != null) {
				try {
					fis.close();                // 리소스 반납
				} catch (IOException e) {
					System.out.println(e);
				}
			}
					System.out.println("항상 수행 됩니다.");	// O
		}
		System.out.println("여기도 수행됩니다.");	// O
	}
}
```
### 3. try - with - resources 문
* 리소스를 사용하는 경우 close() 하지 않아도 자동으로 해체되도록 함.
* 리소스를 try() 내부에서 선언해야 함 

        - java 7 부터 제공
        - java 9 부터 리소스 try() 외부에서 선언하고 변수만 try(obj)와 같이 사용할 수 있음.

* close()를 명시적으로 호출하지 않아도 try{}블록에서 열린 리소스는   
  정상적인 경우나 예외가 발생한 경우 모두 자동으로 해제됨

```
    - 해당 리소스 클래스가 AutoCloseable 인터페이스를 구현 해야 함.
    - FileInputStream의 경우에는 AutoCloseable을 구현하고 있음.
```

```java
public class ExceptionTest {

	public static void main(String[] args) {
		try(FileInputStream fis = new FileInputStream("Hello.txt")){
			
		} catch (FileNotFoundException e) {
				System.out.println(e);
		} catch (IOException e) {
				System.out.println(e);  		// 자동 close()
		}
		System.out.println("여기도 수행 됩니다.");	// O
	}

}
```

#### AutoCloseable 인터페이스 구현

```java
public class AutoCloseObject implements AutoCloseable{

	@Override
	public void close() throws Exception {
		System.out.println("close()가 호출되었습니다.");
	}

}
```
```java
public class AutoCloseTest {

	public static void main(String[] args) {
		
		AutoCloseObject obj = new AutoCloseObject();
		
		try(AutoCloseObject obj2=obj){
			throw new Exception();	// 예외 강제 발생
		} catch (Exception e) {
			System.out.println(e);	// close 호출 O
		}
	}

}
```

### 4. 예외 처리 미루기 (던지기)
* throws를 사용하여 예외처리 미루기
* 예외가 발생한 메서드에서 처리하지 않고 메서드를 호출한 곳으로 예외를 던져 메서드를   
  호출한 부분에서 예외를 처리하는 방법

    	        <-          <-                 <-
    	  JVM       main()      myMethod1()          myMethod2()
     	                                              예외발생 !
*  main()에서 throws를 사용하면 가상머신에서 처리 됨.  

* try{} 블록으로 예외를 처리하지 않고, 메서드 선언부에 throws 추가.

### 5. 하나의 try{} 블록에서 예외가 여러개 발생하는 경우
* 예외를 묶어서 하나의 방법으로 처리할 수도 있음.
* 각각의 예외를 따로 처리할 수도 있음.
* Exception 클래스를 활용하여 default처리를 할때 Exception 
  블록은 맨 마지막에 위치해야 함 

        가장 최상위 클래스인 Exception 클래스는 가장 마지막 블록에 위치해야 함.

```java
package kr.co.ezenac.throwsexception;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class ThrowsException {

	public Class loadClass(String fileName,String className) 
                throws FileNotFoundException, ClassNotFoundException{
		FileInputStream fis = new FileInputStream(fileName);
		Class c = Class.forName(className);
		return c;
	}
	public static void main(String[] args) {
		ThrowsException test = new ThrowsException();		// loadClass에서 던짐
		try {
			test.loadClass("Hello.txt", "java.lang.string");
		} catch (FileNotFoundException e) {
			System.out.println(e);
		} catch (ClassNotFoundException e) {
			System.out.println(e);
		}
		System.out.println("end");
	}

}
```
## 사용자 정의 예외 클래스 활용
* 자바에서 제공하는 예외 클래스외에 프로그래머가 직접 만들어야 하는 예외가  
  있을 수 있음.

* 기본 예외 클래스 중 가장 유사한 예외 클래스에서 상속 받아 만듦.

* 기본적으로 Exception 클래스를 상속해서 만들 수 있음.

*  ex) 매개변수로 전달된 아이디가 null 이거나 8자이하 20자 이상인 경우  
  예외를 발생시키고 예외 클래스를 만들고 예외를 발생시켜라.

```java
public class IDFormatException extends Exception {
	
	public IDFormatException(String message) {	
		super(message);
	}
}
```
```java
public class IDFormatTest {
	
	private String userId;
	
	
	public String getUserId() {
		return userId;
	}


	public void setUserId(String userId) throws IDFormatException {
		
		if(userId == null) {
			throw new IDFormatException("아이디는 null 일수 없다.");
		}
		else if(userId.length()<8||userId.length()>20) {
			throw new IDFormatException("아이디는 8자 이상 20자 이하로 쓰세요");
		}
		this.userId = userId;
	}
	public static void main(String[] args) {
		
		IDFormatTest idtest = new IDFormatTest();
		String myId = null;
		
		try {
			idtest.setUserId(myId);		// null
		} catch (IDFormatException e) {
			System.out.println(e);
		}
		myId = "이순신";					// 8자 안됨
		try {
			idtest.setUserId(myId);
		} catch (IDFormatException e) {
			System.out.println(e);
		}
	}

}
```