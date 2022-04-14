---
title: Java 6.조건문2
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is 조건문?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language
last_modified_at: '2022-03-22 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

switch
=========

## 1. switch - case 문
* if ~ else if ~ else 문을 가독성 좋게 구현
* 비교조건이 특정 값이나 문자열인 경우 사용
* break 문을 사용하여 각 조건이 만족되면 switch 블록을 빠져나오도록 함

```java
 switch(조건식){
        case 1:
            처리 1
            break;
        case 2:
            처리 2
            break;
        default:
            처리 n         
        }
```

```java
import java.util.Scanner;

/*
 *  사용자로부터 월을 입력받아서 
 *  해당 월의 마지막 날짜를 출력하는 프로그램을 작성하시오.
 *  단 2월은 28일로 가정한다.
 *  
 *  예시) 월: 3
 *  	31일까지 입니다.
 */


public class SwitchTest3 {
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		System.out.print("월 : ");
		int month=sc.nextInt();
		
		switch(month) {
			case 1: case 3:	case 5: case 7:	case 8:	case 10: case 12:
				System.out.println("31일까지입니다.");
				break;
			case 4:	case 6:	case 9:	case 11:
				System.out.println("30일까지입니다.");
				break;
			case 2:
				System.out.println("28일까지입니다.");
				break;
			default :
				System.out.println("존재하지 않는 달입니다.");
		}
		sc.close();
	}
}
```

* 조건식

```
    - int 범위 이하의 점수
    - String 값
```

* 조건식의 결과와 일치하는 case문으로 이동 후, break문을  만날때까지 실행함.

```
    - break문이 없으면 switch 문을 벗어나지 않고 계속 실행
    - break문 존재해야함.
```
## 2. Java 14 부터 지원되는 switch 구문

* 간단하게 쉼표(,)로 조건 구분
* 반환값을 받을 수 있음.
* yield 키워드 사용

```java
import java.util.Scanner;

public class SwitchTest4 {

	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		System.out.print("월 : ");
		int month=sc.nextInt();		
		int day =	switch(month) {
			case 1, 3, 5, 7, 8, 10, 12 ->{
			System.out.println("31일 까지 입니다.");
			yield 31;
			}
			case 4,6,9,11 ->{
				System.out.println("30일 까지 입니다.");
				yield 30;
			}
			case 2 ->{
				System.out.println("28일 까지 입니다.");
				yield 28;
			}
			default ->{
				System.out.println("존재하지 않는 달입니다.");
				yield 0;
			}
		};
		
		System.out.println(month+"월은 "+ day + "일입니다.");
		
		sc.close();
	}

}
```