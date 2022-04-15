---
title: Java 9. 반복문
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is 반복문?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java 반복문
last_modified_at: '2022-03-24 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

loop
=======

## 1. for문

* 어떤 조건이 성립하는 동안 반복 처리 실행하는 제어문.

```
    - for 문
    - while 문
    - do ~ while 문
```

### for문을 이용한 반복 

```java
            ① 1     ② 2     ④ 4
        for(초기화식; 조건식; 증감식){
            // 조건식이 true이면 실행될 코드(수행문)  ③ 3
        }    

        첫번째 루프의 흐름 : ① 1 => ② 2 => ③ 3 => ④ 4
        두번째 루프의 흐름 : ② 2 => ③ 3 => ④ 4
        세번째 루프의 흐름 : ② 2 => ③ 3 => ④ 4
```

```java
public class ForTest3 {
	
	public static void main(String[] args) {
	
		// 1에서 100까지의 합중에 누적합계가 2000천 이상 일때 i 값을 출력하시오.
		int sum =0;
		int temp = 0;
		
		for(int i=1;i<=100;i++) {
			sum +=i;
			if(sum>=2000) {
				temp = i;
				break;
			}
			System.out.println("sum : "+sum);
		}
		System.out.println("누적합계가 2000이상 일때 i의 값 : "+temp);
		System.out.println("누적합계가 2000이상 일때 sum의 값 : "+sum);
	}
}
```

### 중첩 for문 (double loop)

```java
        for(초기화식; 조건식; 증감식){
             for(초기화식; 조건식; 증감식){

               }
          }
```

```java
public class Gugudan {

        public static void main(String[] args) {

			for(int i=2; i<10;i++) {
				for(int j=1; j<10; j++) {
					System.out.println(i+" X "+j+" = "+(i*j));
				}
				System.out.println();
			}
	}

}
```

### for문 요소의 생략, 응용

```
        - 증감식에는 보통 ++등 단항식을 이용하는데 산술 연산식도 가능
```

## 2. while문

* 조건이 참(true)인 동안 반복 수행

* 무한 루프에 자주 사용
* 조건이 맞지 많으면 1번도 수행 안될수 있음
* 기본 형태 

```java
        while(조건식){
            // 조건식의 연산결과가 true일때 실행코드

        }                
```

```java
public class WhileTest {

	public static void main(String[] args) {
		
		int sum = 0;
		int i = 1;
		/*
		 *  while문 옆에는 조건식만 들어간다.
		 *  for문에 비해서 일반적으로 반복에서는 가독성이 떨어진다.
		 */
		while(i<=100) {
			sum+=i;
			i++;
			System.out.println(sum);
		}
		System.out.println("1~100까지의 합 : "+sum);
		System.out.println();
		
		/*
		 *  while문은 무한루프용으로 많이 사용함.
		 *  if()문 break문과 함께 무한루프를 벗어날 코드를 작성해 주는게 맞음.
		 */
		int j=1;
		while(true) {
			System.out.println(j);
			if(j>=100) {
				break;
			}
			j++;
		}
		
	}

}
```

## 3. do ~ while 문

* 조건과 상관없이 한번은 수행문을 수행

* 기본 형태

```java
        do{
            수행문 1;
            ....
        }while(조건식);
```

```java
import java.util.Scanner;

public class DoWhileTest {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		System.out.println("메세지를 입력하세요.");
		System.out.println("프로그램을 종료하려면, q를 입력하세요.");
		String str =null;
		
		do {
			System.out.print(">");
			str = sc.nextLine();
			System.out.println("입력받은 메세지 : "+ str);
			
		}while(!str.equals("q"));
		
		System.out.println("프로그램을 종료합니다.");
		
		sc.close();
	}

}
```

## 4. break 문

* 하나의 반복문 or switch문을 빠져 나올때 사용함.

* if문과 함께 사용하여 특정 조건을 만족하면 반복문 벗어나는 용도로 사용함.

## 5. continue 문

* 자신이 포함된 반복문의 끝으로 이동함.

```
        - continue문 이후의 문장은 실행되지 아니함. 다음 반복문 실행함.
        - break문과 달리 반복문을 빠져나가지 않음.
```

```java
public class ContinueTest2 {

	public static void main(String[] args) {
		
		int num =0;
		int count =0;
		
		while((num++)<100) {
			
			if((num % 2) !=0 || (num % 3) !=0)
				continue;
	
			
			count++;
			System.out.println(num);
		}
		System.out.println("count : "+count);
		
		
	}

}
```

## 6. 쓰임

```
 		    while문                     do~while문                        for문
		--------------------------------------------------------------------------------------
		실행   조건이 참인동안 반복               ~~~                   초기화, 조건체크, 증감순
 		     조건이 거짓이면 실행부분      수행문을 먼저 실행하고
 		     이없음.                      조건 체크
		--------------------------------------------------------------------------------------
		     조건식의 결과나 변수가 true                             특정 수의 범위
		쓰임   false인 경우 주로 사용                                횟수와 관련해 반복되는 경우,
		                                                            배열과 함께 많이 사용됨.  
		--------------------------------------------------------------------------------------
```
