---
title: Java 5.조건문
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is 조건문?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language
last_modified_at: '2022-03-21 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

조건문
======

## 1. 조건문이란?
    
* 주어진 조건에 따라 다른 실행이 이루어지도록 구현
* 조건문은 조건식의 결과가 'true인 경우' 와 'false인 경우'의 두가지 흐름을 만들어냄
* if문, switch문 

## 2. if문 문법

```java    
    1) if(조건식) { 수행문;  }                   //조건식 '참'인 경우 수행문이 실행
    2) if ~ else 문

        if(조건식){ 
            수행문 1 ;                 //조건식 '참'인 경우 수행됨
        }else{
                                       // 조건식 '참'이 아닌 경우 수행됨                                
        }    

```

## 3. if ~ else if ~ else 문
- 하나의 상황에 대한 조건이 여러개로 나뉘고 각 존에 다른 수행이 이루어져야 할 경우 사용
- 각조건은 상호 배타적임

```java
    if(조건식1){
        수행문1;                        // 조건식 1 '참'인 경우 수행하고 전체 조건문을 빠져나감
    }    
    else if(조건식2){
        수행문2;                        // 조건식 2 '참'인 경우 수행하고 전체 조건문을 빠져나감
    }
    else if(조건식2){
        수행문3;                        // 조건식 3 '참'인 경우 수행하고 전체 조건문을 빠져나감
    }
    else {
        수행문4;                        // 위조건이 모두 해당되지 않은 경우 수행됨(디폴트 조건)
    }

        수행문5;

            - 가령 조건식2가 만족되면 수행문2 -> 수행문5

```

```java
import java.util.Scanner;

/*
 *  점수를 입력하세요 : 87
 *  
 *  점수가 80~89점 사이입니다.
 *  학점은 B입니다.
 *  
 *  90~100  A
 *  80~89   B
 * 	70~79	C
 * 	70미만	D
 */
public class IfElseIfElse2 {

	public static void main(String[] args) {
		
		Scanner sc=new Scanner(System.in);
		System.out.print("점수를 입력하세요: ");
		int score = sc.nextInt();
		
		// score변수의 값에 따라서 조건문에서 분기가 일어남
		if(score>=90) {
			System.out.println("점수가 90점~100점 사이입니다.");
			System.out.println("학점은 A입니다.");
		}
		else if(score>=80) {
			System.out.println("점수가 80점~89점 사이입니다.");
			System.out.println("학점은 B입니다.");	
		}
		else if(score>=70) {
			System.out.println("점수가 70점~79점 사이입니다.");
			System.out.println("학점은 C입니다.");
		}
		else {
			System.out.println("점수가 70점 미만입니다.");
			System.out.println("학점은 D입니다.");
		}
		sc.close();
		
		
		
	}

}
```

## 4. 중첩 if문
- if문 안에 또 다른 if문 중첩해서 넣을 수 있음.
- 중첩 if문 개수가 제한이 없음 ( 너무 많이 중첩하면 가독성이 저해된다. )

```java
/*
 * 	성별 (1은 남자 2은 여자)
 * 	나이, 신체등급 순으로 입력 받아서
 *  ==> 신체등급 1~3 : 현역
 *  	신체등급 4 : 공익
 *  	그외 :면제가 출력되는 프로그램을 작성하시오.
 *   
 * 	여자 일때에는 추가적인 정보 입력 대신 "여성에게는 국방의무가 없습니다."가 출력되게 작성하시오.
 * 	남자이지만 미성년자일 경우 추가적인 정보 입력 대신 "미성년자에게는 아직 신체등급이 부여되지 않습니다." ~~
 * 
 * 
 */
public class IfNested {
	
	public static void main(String[] args) {
		
		Scanner sc=new Scanner(System.in);
		System.out.print("성별을 입력해주세요 ( 1은 남자 2은 여자) : ");
		int grade=0;
		int gender =sc.nextInt();
		if(gender==1) {
			// 남자이므로 나이를 입력 받는다.
			System.out.print("나이를 입력해주세요 : ");
			int age=sc.nextInt();
			if(age>=19) {
				System.out.print("등급을 입력해주세요 : ");
				 grade =sc.nextInt();
				 if(grade<4) {
					 System.out.println("현역");
				 }
				 else if(grade==4) {
					 System.out.println("공익");
				 }
				 else {
					 System.out.println("면제");
				 }
			}
			else {
				System.out.println("미성년자에게는 아직 신체등급이 부여되지 않습니다.");
			}
		}
		else {
			System.out.println("여성에게는 국방의무가 없습니다.");
		}		
	
		sc.close();
		
		
		
	}
}
```