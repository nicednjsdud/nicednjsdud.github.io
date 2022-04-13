---
title: 자바 I/O 1
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: about java I/O
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, input ,output
last_modified_at: '2022-04-13 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---
자바의 입출력 위한 I/O 스트림
============================

## 1. 입출력 스트림
* 네트웍에서 자료의 흐름이 물과 같다는 의미에서 유래
* 다양한 입출력 장치에 독립적으로 일관성 있는 입출력 방식 제공

```
   - 키보드, 파일디스크, 메모리 등
   - 파일에서의 입출력
   - 모니터의 입출력
   - 그래픽카드, 사운드카드의 입출력
```

* 입출력이 구현되는 곳에서는 모두 I/O 스트림을 이용.

## 2. 입출력 스트림 구분
### 1. I/O 대상 기준

    - 입력 스트림, 출력 스트림

### 2. 자료의 종류

    - 바이트 스트림, 문자 스트림

### 3. 스트림의 기능

    - 기반 스트림, 보조 스트림

## 3. 입력 스트림과 출력 스트림

### 입력 스트림 : 대상으로부터 자료를 읽어 들이는 스트림

* FileInputStream, FileReader

```
자바 응용 프로그램  <---------  자료 
```



### 출력 스트림 : 대상으로부터 자료를 출력하는 스트림
* FileOutputStream, FileWriter

```
    자바 응용 프로그램  --------->  자료
```

## 4. 바이트 단위 스트림, 문자 단위 스트림
---
### 1. 바이트 단위 스트림 : 바이트 단위로 자료를 읽고 씀
        자바 응용 프로그램 ------------ 자료
                          - - - - - - -
                          ------------
                          (바이트 스트림)


* FileInputSteam, FileOutputStream,  
* BufferedInputStream, BufferedOutputSteam
* 동영상, 음악 파일 등

### 2. 문자 단위 스트림 : 문자는 2바이트씩 처리 해야 함
        자바 응용 프로그램 ------------ 자료
                          -- -- -- --
                          ------------
                          (문자 스트림)
* FileReader, FileWriter, BufferedReader, BufferedWriter

## 5. 기반 스트림과 보조 스트림
```
        기반 스트림 + 보조 스트림1 + 보조스트림2
```

### 1. 기반 스트림 : 대상에 직접 자료를 읽고 쓰는 기능의 스트림 

* FileInputStream, FileOutputStream, FileReader, FileWriter

### 2. 보조 스트림 : 직접 읽고 쓰는 기능은 없음
* 추가적인 기능을 제공해 주는 스트림.
* 항상 기반 스트림이나 또 다른 보조 스트림을 생성자 매개변수로 포함함.
* InputStreamReader, OutputStreamWriter 
* BufferedInputStream, BufferedOutputStream

## 6. 표준입출력
### 1. System 클래스의 표준 입출력 멤버
```java
    - public static final PrintStream out;   // 표준 출력 스트림 
        - 모니터
        - System.out.println("메세지");

    - public static final InputStream in;    // 표준 입력 스트림 
        - 키보드
        - System.in.read();                  // 한 바이트 읽기

    - public static final PrintStream err;   // 표준 에러 스트림
        - 에러 출력(모니터)
        - System.err.println("Err Message");
```
---

```java
import java.io.IOException;

public class SystemInTest {

	public static void main(String[] args) {
		System.out.print("알파벳 하나를 쓰고 [Enter]를 누르세요: ");
		
		int i;
		
		try {
			i = System.in.read();		// a
			System.out.println(i);		// 97
			System.out.println((char)i); // char형으로 변환 a
		} catch (IOException e) {
			e.printStackTrace();
		}

	}

}
```
## 7. Scanner 클래스
* 입력 클래스
* 문자뿐 아니라 정수, 실수등 다양한 자료형을 읽을 수 있음

## 8. Console 클래스
* console에서 표준 입출력이 가능
* 이클립스와는 연동이 안됨

```java
import java.io.Console;

public class ConsoleTest {

	public static void main(String[] args) {
		
		Console console = System.console();
		System.out.print("이름 : ");
		String name=console.readLine();
		
		System.out.println("비밀번호 : ");
		char[] password = console.readPassword();
		
		System.out.println(name);
		System.out.println(password);
	}

}
```

```cmd
    이름 : Hello
    비밀번호 :

    Hello
    1212
```
