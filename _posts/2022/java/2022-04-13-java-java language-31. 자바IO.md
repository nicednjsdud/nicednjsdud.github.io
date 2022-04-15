---
title: Java 27. 자바I/O 2
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
meta_keywords: java,java language, input, output
last_modified_at: '2022-04-13 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

자바IO
=======

# 1. 바이트 단위 입출력 스트림
## 1. InputStream
* 바이트 단위 입력 스트림 최상위 클래스
* 많은 추상 메서드가 선언되어 있고 이를 하위 스트림이 상속받아 구현함
### 주요메서드
### int read()

```    
- 입력 스트림으로부터 한 바이트의 자료를 읽어들임.
- 읽은 자료의 바이트 수를 반환함.
```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileInputStreamTest2 {

	public static void main(String[] args) {
		FileInputStream fis = null;
		
		try {
			fis = new FileInputStream("input.txt");
			int i;
			while((i = fis.read()) != -1) {
			System.out.print((char)i);	//마지막까지 출력
			}
			
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				fis.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		System.out.println("end");
	}

}
```
#### 줄이기
```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileInputStreamTest3 {

	public static void main(String[] args) {
		 
		try(FileInputStream fis=new FileInputStream("input.txt")) {
			int i;
			while((i = fis.read()) != -1) {
			System.out.print((char)i);	//마지막까지 출력
			}	
		} catch (Exception e) {
			e.printStackTrace();
		} 
		System.out.println("end");
	}

}
```


### int read (byte[] b)

            - 입력 스트림으로부터 b[] 크기의 자료를 b[]에 읽어들임.

### int read (byte[] b, int off, int len)

            - 입력 스트림으로부터 b[] 크기의 자료를 off변수 위치로부터 len
              만큼 읽어들임
### void close()

            - 입력 스트림과 연결된 대상의 리소스를 닫음          

```java
import java.io.FileInputStream;

public class FileInputStream4 {

	public static void main(String[] args) {
		
		try(FileInputStream fis = new FileInputStream("input.txt")){
			int i;
			byte[] bs = new byte[10];
			while((i=fis.read(bs)) != -1) {
//				for(byte b : bs) {
//					System.out.print((char)b);	//쓰레기 값까지 나옴
//				}
				for(int k=0;k<i;k++) {
					System.out.print((char)bs[k]);// 읽은 만큼만 출력
				}
				
				System.out.println();	
			}
			
			
		}catch(Exception e) {
			System.out.println(e);
		}
	}

}
```

## 2. OutputStream
* 바이트 단위 출력 스트림 최상위 클래스

```java
import java.io.FileOutputStream;

public class FileOutputStreamTest {

	public static void main(String[] args) {
		
		try(FileOutputStream fos =new FileOutputStream("output.txt",true)){
			fos.write(65);
			fos.write(66);
			fos.write(67);	//output.txt = ABC찍힘
		}catch(Exception e) {
			System.out.println(e);
		}
	}

}
```

* byte[] 배열에 A-Z까지 넣고 배열을 한꺼번에 파일에 쓰기

```java
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
public class FileOutputStreamTest2 {

	public static void main(String[] args) throws FileNotFoundException {
		FileOutputStream fos = new FileOutputStream("output2.txt", true);
		
		try(fos){
			byte[] bs = new byte[26];
			byte data = 65;				// 'A'의 아스키 값
			for(int i=0;i<bs.length;i++) {
				bs[i] = data;
				data++;
			}
			fos.write(bs);	// 배열 한꺼번에 출력하기
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		System.out.println("출력이 완료되었습니다.");
	}	

}
```

```
output2.txt

ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

* byte[] 배열의 특정 위치에서부터 정해진 길이만큼 쓰기

```java
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamTest2 {

	public static void main(String[] args) throws FileNotFoundException {
		
		try(FileOutputStream fos = new FileOutputStream("output3.txt")){
			byte[] bs = new byte[26];
			byte data = 65;				// 'A'의 아스키 값
			for(int i=0;i<bs.length;i++) {
				bs[i] = data;
				data++;
			}
			fos.write(bs, 2, 10);	// 배열의 2번째 위치부터 10개 바이트 출력하기
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		System.out.println("출력이 완료되었습니다.");
	}	

}
```

```
output3.txt

CDEFGHIJKL
```
* Input Output 같이쓰기

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputTest {
	
	public static void main(String[] args) {
		
		byte[] bs = new byte[26];
		byte data = 65;
		for(int i=0; i<bs.length;i++) {
			bs[i]=data;
			data++;	
		}
		try(FileOutputStream fos = new FileOutputStream("Hello.txt",true);
			FileInputStream fis = new FileInputStream("Hello.txt")){
			
			fos.write(bs); // Hello.txt로 쓰고
			int ch;
			while((ch = fis.read()) !=-1) {
				System.out.print((char)ch);	// Hello.txt 읽음
			}
			
		}catch(IOException e) {
			System.out.println(e);
		}
	}
}
```

# 2. 문자 단위 입출력 스트림
## 1. Reader
* 문자 단위 입력 스트림 최상위 추상 클래스
* 많은 추상 메서드가 선언되어 있고 이를 하위 스트림이 상속받아 구현함

### ***주요 하위 클래스***

### - File Reader

```
	- 파일에서 문자 단위로 읽는 스트림 클래스임
```

```java
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class FileReaderTest2 {

	public static void main(String[] args) {

		try (FileReader fis=new FileReader("reader.txt")){
			int i;
			while((i = fis.read()) != -1) {
				System.out.print((char)i);
			}
			
		} catch (IOException e) {
			e.printStackTrace();
		} 		
	}

}
```

### - InputStreamReader

```
	- 바이트 단위로 읽은 자료를 문자로 변환해주는 보조 스트림 클래스임
```

### - BufferedReader

```
	- 문자로 읽을 때 배열을 제공하여 한꺼번에 읽을 수 있는 기능을 제공하는 보조스트림
```

### ***주요 메서드***

### - int read()

```
	- 파일로 부터 한 문자를 읽습니다. 읽은 문자를 반환함.
```

### - int read (char[] cbuf)

```
	- 파일로부터 cbuf 배열에 문자를 읽어들임.
```

### - int read (char[] cbuf, int off, int len)

```
	- 파일로부터 cbuf 배열의 off위치로부터 len 개수만큼의 문자를 읽어들임.
```

### - void close()

```
	- 입력 스트림과 연결된 대상 리소스를 닫음.
```

## 2. Writer
* 문자 단위 출력 스트림 최상위 추상 클래스
* 많은 추상 메서드가 선언되어 있고 이를 하위 스트림이 상속받아 구현함

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterTest {

	public static void main(String[] args) throws IOException {
		
		FileWriter fw = new FileWriter("writer.txt");
		fw.write('A');	// 문자 하나 출력
		
		char buf[]= {'B','C','D','E','F'};
		fw.write(buf); 	// 문자 배열 출력
		
		String str="안녕하세요. 잘 써지고 있죠";
		fw.write(str);	// String 출력
		
		fw.write(buf, 1, 2);// 문자 배열의 일부 출력
		fw.write("65"); 	// 숫자 그대로 출력
		
		fw.close();
		
		
		
	}

}
```

```
 writer.txt

 ABCDEF안녕하세요. 잘 써지고 있죠CD65
``` 

### ***주요 하위 클래스***

### - FileWriter

```
	- 파일에서 문자 단위로 출력하는 스트림 클래스.
```

### - OutputStreamWriter

```
	- 바이트 단위의 자료를 문자로 변환해 출력해주는 보조 스트림 클래스.
```

### - BufferedWriter

```
	- 문자로 쓸 떄 배열을 제공하여 한꺼번에 쓸 수 있는 기능을 제공하는 보조 스트림
```

### ***주요 메서드***

### - void write(int c)

```
	- 한 문자를 파일에 출력함
```

### - void write(char[] cbuf)

```
	- 문자 배열 cbuf의 내용을 출력함
```

### - void write(char[] cbuf, int off, int len)

```
	- 문자 배열 cbuf의 off위치에서부터 len개수의 문자를 출력함
```

### - void write(String str)

```
	- 문자열 str을 출력함
```

### - void write (String str, int off, int len)

```
	- 문자열 str의 off번째 문자로부터 len 개수만큼 출력함.
```

### - void flush()

```
	- 출력하기 전에 자료가 있는 공간 (출력 버퍼)을 비워 출력하도록 함
```

### - void close()

```
	- 스트림과 연결된 리소스를 닫음. 출력 버퍼도 지워짐
```