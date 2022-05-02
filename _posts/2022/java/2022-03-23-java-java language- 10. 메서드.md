---
title: Java 7. Method
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is Method?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java Method
last_modified_at: '2022-03-23 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

메서드
=======

## 1. 자주 쓰는 메서드 - Math.random()
### 1) 특정 범위의 정수 난수 얻기

```java
        0.0 <= Math.random() < 1.0
```

### 2) 0 ~ 10 까지의 임의의 정수 얻기

```java
        0.0 * 10 <=(Int)Math.random() * 10 < 1.0 * 10
----------------                      ---------------
         0.0    (0,1,2,3,4,5,6,7,8,9)        10.0
-----------------------------------------------------

     0.0 * 10 + 1 <=(Int)Math.random() * 10 + 1<(int) 1.0 * 10 + 1
----------------                           ---------------          
        1.0     (1,2,3,4,5,6,7,8,9,10)        11

```

### 3) 공식

```java
        int num = (int)( Math.random() * n ) + start         

        ex) 주사위 번호 뽑기
            int num =(int)( Math.random()* 6 ) + 1

            로또 번호 뽑기
            int num =(int)( Math.random()* 45 )+ 1

```

## 2. 메서드  

* 함수 (function)
* 클래스 안에 존재하는 함수
* 수학에서의 함수 

```
        숫자1, 숫자2            
            ||                                                  
            \/                                        
        -----------
        |         |
        |  더하기 |                                             
        |   함수  |                                         
        -----------                                                             
                ||                                              
                \/                                                         
                숫자의 합                                                           

```

* 자바에서의 함수                                                       

```
        num1, num2
            ||
            \/
        -------------
        |           |
        |  addNum() |
        |           |
        -------------                
                ||
                \/
                result
```

###  메서드 정의 

```java
        int addNum(int num1,int num2)            
        {
            int reult = num1 + num2;
            return result;
        }

```

### main 메서드 : 프로그램 시작 (entryPoint)

```java
                     반환형 메서드이름      매개변수
                     ----- ---- -------------- 
        public static void main(String[] args)
        {
           System.out.println("이순신");
           hello(12);
           hello(13);
        }   

        public static void hello(int age){
            System.out.println("안녕하세요.");
        }
```

* 메서드 종료하기

```
     - return : 어떤 값을 반환하는 데 사용하는 예약어    
```