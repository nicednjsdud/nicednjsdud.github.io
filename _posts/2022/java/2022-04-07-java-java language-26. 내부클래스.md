---
title: Java 25. 내부 클래스(Inner Class) 
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is Inner Class?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, inner class
last_modified_at: '2022-04-07 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---
내부클래스 (Inner class)
==========================
### 1. 클래스 내부에 구현한 클래스 (중첩된 클래스)
### 2. 클래스 내부에서 사용하기 위해 선언하고 구현하는 클래스.
    - 클래스 내부에 선언한 클래스로 이 클래스를 감싸고 있는 외부 클래스와  
      밀접한 연관이 있는 경우가 많음.

    - 다른 외부 클래스에서 사용할 일이 거의 없는 경우에 내부클래스로 선언 해서 사용

### 3. 주로 외부 클래스 생성자에서 내부 클래스를 생성
### 유형
    - 인스턴스 내부 클래스
    - 정적 내부 클래스
    - 지역 내부 클래스
    - 익명(Anonymous) 내부 클래스

## 1.인스턴스 내부 클래스
### 1. 내부적으로 사용할 클래스를 선언 (private으로 선언하는 것을 권장)
### 2. 외부 클래스가 생성된 후 생성됨

```java
class OutClass{
	private int num = 10;
	private static int sNum = 20;
	private InClass inClass;
	
	public OutClass() {
		inClass = new InClass();	// 내부 클래스 생성
	}	
	class InClass{
		int inNum = 100;
//		static int sInNum = 200;	// Err
		void inTest() {
			System.out.println("OutClass num = "+num+"(외부 클래스의 인스턴스 변수)");
			System.out.println("OutClass sNum = "+sNum+"(외부 클래스의 static 변수)");
			System.out.println("InClass inNum = "+inNum+"(내부 클래스의 인스턴스 변수)");
		}
//		static void sTest() {}      // Err
	}
	public void usingInClass() {
		inClass.inTest(); 			// 내부 클래스 참조변수를 사용하여 메서드 호출하기
	}
}
public class InnerTest {
	public static void main(String[] args) {
		OutClass outClass = new OutClass();
		System.out.println("외부 클래스 이용하여 내부 클래스 기능 호출");
		outClass.usingInClass(); // O		

        OutClass.InClass inClass = outClass.new InClass();	
		System.out.println("외부 클래스를 이용하여 내부클래스 생성");
		inClass.inTest(); // O
	}
}
```

## 2.정적(static) 내부 클래스
### 1. 외부 클래스 생성과 무관하게 사용할 수 있음.
### 2. 정적 변수, 정적 메서드 사용

```java
class OutClass{
	private int num = 10;
	private static int sNum = 20;

	public OutClass() {	}

	static class InStaticClass{
		int inNum = 100;
		static int sInNum = 200;	

		void inTest() {		// 정적 클래스의 일반 메서드
			// num +=10;	// 외부 클래스의 인스턴스 변수는 사용불가
	System.out.println("InStaticClass inNum ="+inNum+"(내부 클래스의 인스턴스 변수 사용)");
	System.out.println("InStaticClass sInNum ="+sInNum+"(내부 클래스의 스태틱 변수 사용)");
			System.out.println("OutClass sNum ="+sNum+"(외부 클래스의 스태틱 변수 사용)");
		}

		static void sTest() {	//정적 클래스의 static 메서드
			// num+=10;			//외부클래스의 인스턴스 변수는 사용할 수 없음
			// inNum+=10;		//내부 클래스의 인스턴스 변수는 사용할 수 없음
			System.out.println("OutClass sNum ="+sNum+"(외부 클래스의 스태틱 변수 사용)");
			System.out.println("InStaticClass ="+sInNum+"(내부 클래스의 스태틱 변수 사용)");		
		}
	}
}	

public class InnerTest {
	public static void main(String[] args) {
		// 외부 클래스 생성하지 않고 바로 정적 내부 클래스 생성
		OutClass.InStaticClass sInClass = new OutClass.InStaticClass();
		System.out.println("정적 내부 클래스의 일반 메서드 호출");
		sInClass.inTest(); // O
		
		System.out.println("정적 내부 클래스의 스태틱 메서드 호출");
		OutClass.InStaticClass.sTest(); // O
	}
}
```
## 3.지역 내부 클래스
### 1. 지역 변수와 같이 메서드 내부에서 정의하여 사용하는 클래스
### 2. 메서드의 호출이 끝나면 메서드에 사용된 지역변수의 유효성은 사라짐
### 3. 메서드 호출 이후 사용해야 하는 경우가 있을 수 있으므로 지역 내부  클래스에서 사용하는
###  메서드의 지역변수나 매개변수는 final로 선언됨.
```java
class Outer{
	int outNum = 100;
	static int sNum = 200;
	
	Runnable getRunnable(/*final*/ int i) {		// 지역 변수 - 메서드 호출후 끝날때까지 유효함
		/*final*/ int num = 100;				// 지역 변수 - 메서드 호출후 끝날때까지 유효함
		
		class MyRunnable implements Runnable{
			@Override
			public void run() {			// 내부 객체를 생성한 후 언제든 다시 호출 가능
//				num = 200;				// Err 이때 local변수는 유효하지 않은 상태
//				i = 10;					// Err 값 재할당 불가
				System.out.println(num);
				System.out.println(i);
				System.out.println(outNum);
				System.out.println(Outer.sNum);
			}
		}
		return new MyRunnable();
	}
}
public class LocalInnerClassTest {

	public static void main(String[] args) {
		Outer outer = new Outer();
		Runnable runnable = outer.getRunnable(30);	// 로컬 변수는 호출후 유효하지 않게됨
		runnable.run();							
	}

}
```
## 4.익명(Anonymous) 내부 클래스
### 1. 이름이 없는 클래스 ( 지역 내부 클래스의 클래스 이름은 실제로 호출되는 경우가 없음)
### 2. 클래스 이름을 생략하고, 주로 하나의 인터페이스나 하나의 추상 클래스를 구현하여 반환.
### 3. 인터페이스나 추상클래스 자료형의 변수에 직접 대입하여 클래스를 생성하거나 지역 내부
### 클래스의 메서드 내부에서 생성하여 반환할수 있음.
### 4. 안드로이드 widget의 이벤트 핸들러에 활용됨.
    ex)
        button.setOnClickListener(new View.onClickListener(){
            public boolean onClick(View v){
              ~~~~~
            }
        });
		
```java
Runnable getRunnable(/*final*/ int i) {		// 지역 변수 - 메서드 호출후 끝날때까지 유효함
		/*final*/ int num = 100;				// 지역 변수 - 메서드 호출후 끝날때까지 유효함
		
		return new Runnable(){  // 바로 반환
			@Override
			public void run() {			// 내부 객체를 생성한 후 언제든 다시 호출 가능
//				num = 200;				// Err 이때 local변수는 유효하지 않은 상태
//				i = 10;					// Err 값 재할당 불가
				System.out.println(num);
				System.out.println(i);
				System.out.println(outNum);
				System.out.println(Outer.sNum);
			}
		};		//; 붙이기
	
	}
	Runnable runner = new Runnable() {
		
		@Override
		public void run() {
			System.out.println("Test!");
		}
	};        
```  
```java
public class LocalInnerClassTest {

	public static void main(String[] args) {
		Outer outer = new Outer();
		Runnable runnable = outer.getRunnable(30);	// 로컬 변수는 호출후 유효하지 않게됨
		runnable.run();	
		System.out.println();
		outer.runner.run();     //
	}
}
```
