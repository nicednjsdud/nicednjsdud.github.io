---
title: Java 2.console IO
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is console
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java console
last_modified_at: '2022-03-17 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

## 출력 환경
*  CLI (Command-Line Interface)
*  GUI (Graphics User Interface)

## printf() 사용형식

*  System.out.printf("포맷 문자열",데이터,데이터,...)

```
     -System.out.printf("정수: %d, 실수 : %f, 글자 : %c, 글자들 : %s",)
```        

* ex 1)

```java
public class Printf {
	public static void main(String[] args) {
		
		String name = "Adimral Yi";
		int age = 20;
		double height = 189.5;
		
		System.out.println(age);
		
		System.out.printf("%s의 나이는 %d이고, 키는 %f 입니다. \n",name,age,height);
		System.out.printf("%s의 나이는 %d이고, 키는 %.2f 입니다.", name,age,height);
	}
}
```

* ex 2)

```java
public class Printf3 {

	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		
		System.out.println("문자열을 입력하고 엔터를 치세요. ");
		String name1 = scan.nextLine();					//줄단위 입력처리
		System.out.println("문자열을 입력하고 엔터를 치세요. ");
		String name2 = scan.next();						//공백이나 탭 단위 처리
		String name3 = scan.next();
		String name4 = scan.next();
		
		System.out.printf("[%s] [%s] [%s] [%s]",name1,name2,name3,name4);
		
		
		scan.close();
		
	}

}
```