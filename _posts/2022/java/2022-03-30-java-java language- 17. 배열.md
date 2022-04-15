---
title: Java 15. Array
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is array?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java array
last_modified_at: '2022-03-30 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Array
======

## 1.배열(Array)이란 ?

* 자료를 순차적으로 한꺼번에 관리하는 방법
* 동일한 자료형의 순차적 자료 구조(Data Structure)
* 인덱스 연산자 []를 이용하여 빠른 참조가 가능
* 물리적 위치와 논리적 위치가 동일 
* 배열의 순서는 0부터 시작
* 많은 데이터 양을 다룰 때 유용하며, 컬렉션 프레임워크의 기초가 됨.

## 2.배열 선언과 초기화


### 1)배열 선언하기

* 1차원 배열 ( 타입이 같은 둘 이상의 데이터를 저장할수 있는 1차원 구조의 메모리 공간 )

```java
   * 자료형[] 변수이름 = new 자료형[개수] 
     자료형 변수이름[] = new 자료형[개수]  
       - int[] arr1 = new int[10];
         int arr1[] = new int[10];
```

### 2)배열 초기화 하기

* 배열은 선언과 동시에 자료형에 따라 초기화됨(정수는 0,실수는 0.0,객체는 null)
* 필요에 따라 초기값을 지정할 수 있음.

```java
     int[] numbers = new int[] {10, 20, 30};        // 개수 생략 해야 함 
     int[] numbers = {10, 20, 30};                  // new int[] 생략 가능

     int[] ids; 
     ids = new int[] {10, 20, 30};      // 선언후 배열 생성 new int[] 생략 불가
```

### 3)배열 사용하기

* [] 인덱스 연산자 활용 -- 메모리 위치를 연산하여 찾아줌
* 배열의 길이와 요소의 개수는 동일하지 않음.

```
   - 배열 선언 시 개수만큼 메모리가 할당되지만,실제요소(데이터)가 없는 경우도있음.
```

* length 속성 : 배열의 개수 반환 

    
## 3.향상된 for문 사용하기

* 배열의 n개 요소를 0부터 n-1까지 순차적 순회할때 간단하게 사용할 수 있음

```
    for(변수 : 배열){
            }
```

```java
public class CharArray {

	public static void main(String[] args) {
		
		char[] alphabet =new char[26];
		char ch = 'A';
		
		for(int i=0;i<alphabet.length;i++) {
			alphabet[i] = ch++;
			
		}
		for(char alpha : alphabet) {
			System.out.println(alpha+", "+(int)alpha);
		}
	}

}
```

## 4.다차원 배열
  
* 2차원, 3차원 배열 등.
* []의 개수가 차원의 수를 의미함.
* 선언방법 

```
        타입[][] 배열이름;
        타입 변수이름[][];
        타입[] 변수이름[];
```

* 배열 초기화

```
        int[][] array = new int[5][5];
        int[][] array2 = new int[][] { {},{} };
```

* 가변 배열 (열이 서로 다른 배열)     

```java
public class TwoDArray {

	public static void main(String[] args) {
		
		//[][]대괄호의 갯수가 곧 차원을 의미함.
		int[][] score = new int[][] {
			{100,100,100},
			{50 ,50 ,50 },
			{10 ,20 ,30 },
			{60 ,20 ,40 }
		};
		// 2차원 배열의 값 읽고 쓰기 위해서는 더블루프가 반드시 필요함
		for(int i=0; i<score.length;i++) {
			for(int j=0; j<score[i].length;j++) {
				System.out.print(score[i][j]+" ");
			}
			System.out.println();
		}
		System.out.println("2차원 배열의 주소 : "+score);
		System.out.println("2차원 배열의 크기 : "+score.length);
		
		for(int i=0;i<score.length;i++) {
			System.out.println("1차원 배열의 주소값 : "+score[i]);
			System.out.println("1차원 배열의 크기 : "+score[i].length);
		}
	}

}
```

## 5.객체 배열

* 요소가 되는 객체의 주소(4바이트)가 들어갈 메모리만 할당되고(null) 각 요소 객체는 생성하여 저장해야함.
* 객체 배열 복사하기 

```
- System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)   
```

- 복사 원본의 위치 : 배열 src의 인덱스 srcPos
- 복사 대상의 위치 : 배열 dest의 인덱스 destPos
- 복수할 요소의 수 : length

- 얕은 복사

```
   - 객체 주소만 복사됨
   - 두 배열이 같은 객체를 가리킴
   - 배열의 요소를 수정하면 같 수정됨.     
```    

- 깊은 복사

```
   - 각각의 객체를 생성하여 그 객체의 값을 복사하여 배열이 서로 다른 객체를 가리키도록 함.
```           

```java
public class ObjectArrayCopy {

	public static void main(String[] args) {
		
		Book[] book = new Book[5];
		Book[] copyBook = new Book[5];
		
		book[0] = new Book("Go 프로그래밍 쿡북", "예런 토레스");
		book[1] = new Book("Go 프로그래밍 쿡북1", "예런 토레스1");
		book[2] = new Book("Go 프로그래밍 쿡북2", "예런 토레스2");
		book[3] = new Book("Go 프로그래밍 쿡북3", "예런 토레스3");
		book[4] = new Book("Go 프로그래밍 쿡북4", "예런 토레스4");
		
		
		System.arraycopy(book, 0, copyBook, 0, book.length);
		
		
		book[0].setTitle("데이터 플랫폼 설계와 구축");
		book[0].setAuthor("다닐 즈부리브스키");
		
		System.out.println("===========book===========");
		for(Book book1 : book) {
			book1.showInfo();
		}
		System.out.println("=========copyBook=========");
		for(Book copyBook1 : copyBook) {
			copyBook1.showInfo();
		}
	}

}
```