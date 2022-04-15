---
title: Java 23. 자바 기본 클래스
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is java class?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java class
last_modified_at: '2022-04-05 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

자바 기본 클래스
=================

## 객체 지향 프로그래밍

### 1)추상화(Abstraction)와 일반화
* 어떤 영역에서 필요로 하는 속성이나 기능을 추출하는 작업
* 데이터 구조, 표현방법에 대한 추상화
* 추상화의 의도는 단순화이며, 일반화의 의도는 공통점을 뽑는 것

### 2)캡슐화(Encapsulation)
* 데이터를 감싸서 외부에서 사용 가능한 부분만 제공 (information hiding)
* 사용하는 코드(클라이언트 코드)가 세부적인 사항을 알 필요가 없음.
* private : 나만 볼수 있는 것, 같은 클래스 내부에서만 접근이 가능함.


### 3)상속성(Inheritance)
* 일반적인(general) 개념의 객체에서 보다 구체적인(specific) 개념의 객체의 관계를 표현
* 상위 클래스 속성과 기능을 하위 클래스에서 사용하거나 재정의 할수 있음.

### 4)다형성(Polymorphism)
   * 같은 메시지, 같은 구현에 대해 각 객체가 다른 표현과 결과를 나타내는 것.
   * 조상 타입으로 자손 타입의 객체들을 접근할 수 있는 것. 

## java.lang 클래스

* 프로그래밍시 import하지 않아도 자동으로 import 됨

```
    - 많이 사용하는 기본 클래스들이 속한 패키지 
```
### Object
- 모든 클래스는 상속받음

#### toString() 메서드
- 생성된 객체의 클래스명과 해시 코드 보여줌
- 보통은 객체 정보를 String으로 바꿔서 사용할때 많이 사용됨.(재정의)
- equals() 메서드   

### String, StringBuffer, StringBuilder
     
### Number, Integer, Long, Float, Double
#### 래퍼 클래스 (Wrapper class)
- 기본 데이터형 (정수형, 문자형,논리형)에 대응하는 클래스
- 기본 자료형에 대해서 객체로서 인식되도록 '포장' 했다.
- 다양한 메서드 추가 

```
    - 값 변환, 형변환, 진법 변환
    - 상수 (MAX_VALUE, MIN_VALUE)
    - 컬렉션 프레임워크에서 사용
```

#### 문자열 변환   
- 각각 문자열을 수치형으로 변환하는 메서드

```java
    - parseByte() : 문자열을 byte형으로 반환
    - parseInt()
    - parseDouble()
```
-  박싱과 언박싱

```java
    - 기본 타입 : byte, short, int ~
    - 래퍼클래스: Byte, Short, Integer ~
```

### System

### Math

```
    - 모두 static으로 선언
```

### Thread

## 가변 인수 (variable length argument)
* 인수 개수가 가변적인 것

```
    - 말줄임표 ...
```

```java
public class VarArgsTest {
	
	public static void helloEzen(String...args) {		// 가변인수 표시
		for(String str : args) {
			System.out.print(str +"\t");
		}
		System.out.println();
	}
	
	public static void main(String[] args) {
		helloEzen("이순신");		
		helloEzen("이도","이방원");				//중복가능
		helloEzen("이도","이방원","이순신");
	}

}
```

## 어노테이션
* 자바 소스 코드에 추가하여 사용할수 있는 메타 데이터의 일종임   

### @ 기호를 앞에 붙여서 사용
- @Override
- @Deprecated

```
    - 이 어노테이션이 적용된 메서드는 문제의 발생 소지가 있거나
      개선된 기능의 다른 것으로 대체되어서 더이상 사용 권장하지 않음.

    - 호환성 유지를 위해서 존재하지만 이후에 사라질수 있는 클래스 또는 메서드
```

- @SuppressWarnings

```
    - Deprecated 관련 경고 등 특정 메세지를 지정하면 해당 경고 메세지를 출력하지 말라는 의미.
```          

```java
interface Unit{
	
	@Deprecated
    @SuppressWarnings("deprecated")
	void move(String str);			// 판단하라
	void run(String str);
}

class Horse implements Unit{        // interface 구현

	@Override
	public void move(String str) {	// 사용하는데 큰 문제없음
		System.out.println(str);
	}

	@Override
	public void run(String str) {
		System.out.println(str);
	}
	
}
public class DeprecatedTest {

    @SuppressWarnings("deprecated")   // 그것과 관련된 경고를 표시하지 x
	public static void main(String[] args) {
		Unit unit =new Horse();
		unit.move("이동합니다."); 		// 취소선으로 표시됨
		unit.run("달립니다.");
	}

}
```

## String 클래스

### 1. 선언하는 두가지 방법
```java
public class StringTest {

	public static void main(String[] args) {
		// new 연산자와 문자열 리터럴 매개변수가 있는 생성자를 이용
		String str1 = new String("오늘은 금요일입니다."); //첫번째 방법
		
		// 문자열 리터럴을 직접 대입함
        // 상수로 리터럴 
		String str3 ="오늘은 금요일입니다.";				 //두번째 방법
	}

}
```
* 문자열 리터럴을 직접 대입하여 만들어진 객체 ( 두번째 방법 )
* String Constant Pool이라는 곳에 분리해서 따로관리한다.
* 같은 객체를 참조한다.
- new 연산자 ( 첫번째 방법 )

### 2. 문자열형 변수의 참조 비교
- == (비교연산자)
- 객체가 가진 문자열의 내용을 비교하는것이 아니라 같은 객체인지 아닌지를 비교

### 3. 문자열형 변수의 내용 비교

- equals()
- compareTo()

```java
public class StringContentTest {

	public static void main(String[] args) {
		String str1 = new String("Apple");	// 대문자	
		String str2 = new String("apple");	// 소문자
		
		//인스턴스 내용 비교
		if(str1.equals(str2)) 
			System.out.println("두 문자열은 같습니다.");
		else
			System.out.println("두 문자열은 다릅니다.");	 // O
		
		// 대소문자 안따진다.
		if(str1.compareToIgnoreCase(str2)==0) 
			System.out.println("두 문자열은 같습니다."); // O
		else
			System.out.println("두 문자열은 다릅니다.");
		
		// 대소문자 구분 비교 (사전순으로 비교)
		int cmpResult = str1.compareTo(str2);
		if(cmpResult==0)
			System.out.println("두 문자열은 일치합니다.");
		else if(cmpResult<0)
			System.out.println("사전의 앞에 위치하는 문자: "+str1);	// O 
		else {
			System.out.println("사전의 앞에 위치하는 문자: "+str2);
		}		
	}
}
```
### 4. 메서드
- 문자열 연결
   - concat()
- 문자열에서 문자찾기
   - indexof()
- 문자열 자르기
   - substring()
- 지정한 문자 반환
   - char charAt(int index)
- 문자열 포함여부 조사
   - boolean contains(String s)
- 시작하는 문자열 s인지 조사
   - boolean startsWith(String s)
- 문자열 앞뒤에 있는 공백 제거
   -  String trim() 
              
```java
public class ConcatIndexOf {

	public static void main(String[] args) {
		//concat
		String str1 = "기초";
		String str2 = "프로그래밍";		// String끼리 합치기
		
		String str3=str1.concat(str2);	// 합한것을 str3에 할당

		System.out.println(str3);       // 기초프로그래밍
		
		String str4 = "자바".concat(str3);// 문자열 리터럴과 String합치기

		System.out.println(str4);       // 자바기초 프로그래밍
		
		//IndexOf
		String str5 = "AppleBananaOrange";
		int num1 = str5.indexOf("a");		// "a"위치 반환
		int num2 = str5.indexOf("a", num1+1); // 찾을 문자열, 시작할 위치
		System.out.println(num2); 			
	}
}
```

```java
public class SubString {

	public static void main(String[] args) {
		String str1 = "AppleBananaOrange";
		int num1 = str1.indexOf("Banana");		//5
		int num2 = str1.indexOf("Orange");		//11
		
		String str2= str1.substring(num1,num2);	// 5 ~ 10
		System.out.println(str2); 				//Banana
		
		String str3 = str1.substring(num2);
		System.out.println(str3); 				// 11 ~
	}

}
```

## StringBuilder, StringBuffer

* 기능 동일
* 한번 생성된 String은 불변 (immutable)하지만
* 내부적으로 가변적인 char[]를 멤버변수로 가짐.

```
   - 문자열을 여러번 연결하거나, 변경할때 사용하면 유용함.
```

* StringBuffer는 멀티 쓰레드 프로그래밍에서 동기화 (Synchronization) 를 보장   

```
   StringBuilder는 단일 쓰레드 프로그램에서 사용 권장.
```

```java
public class StringBuilderTest {

	public static void main(String[] args) {
		// 임시공간
		StringBuilder buffer = new StringBuilder("학교종이 땡땡땡")	;
		
		buffer.append(" 어서모이자.");			// 뒤에 붙이기
		System.out.println(buffer.toString());// 학교종이 땡떙땡 어서모이자
		
		buffer.append(12345);
		System.out.println(buffer.toString());// 학교종이 떙떙떙 어서모이자 12345
		
		buffer.delete(0, 4);				//삭제 0부터 4까지
		System.out.println(buffer.toString());//땡땡땡 어서모이자 12345
		
		buffer.replace(4, 8, "ABC"); 		// 4~7 까지 바꾸기
		buffer.reverse();					// 순서거꾸로
	}

}
```   
