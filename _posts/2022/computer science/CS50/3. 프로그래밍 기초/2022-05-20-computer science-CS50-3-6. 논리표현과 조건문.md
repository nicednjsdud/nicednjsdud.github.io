---
title: CS50 3-6강 논리표현과 조건문
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 논리표현과 조건문
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-17 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

논리표현과 조건문
=================

## 부울 연산식과 조건문

* 프로그래머들이 프로그램에서 특정 코드가 특정 상황에서만 실행되도록 의사  
  결정을 하는 코드를 만들 때 조건문을 쓴다.
* 조건문은 대게 어떠한 값이 참인지 거짓인지를 나타내는 부울 연산식을 통해 작동

## 부울 연산자

![alt](/assets/images/post/computer science/CS50/1/35.png)

* 참과 거짓을 판단하는 부울연산식을 만드는데 사용된다.
* < , > , == , <= , =>
* 두 부울 값을 비교할 수 있다. 3해으이 &&연산자는 '그리고'라는 의미로 둘다  
  참일 떄만 참의 값을 가질 수 있다. 반대로 4번 줄 ||연산자는 '또는'의 의미로  
  둘 중 하나만 참이어도 참의 값을 갖는다.
* 수학에서 같다는 연산자는 =이지만, 대부분의 프로그래밍 언어에서 같다는   
  의미를 갖는 부울 연산자는 ==이다.

```
    = 기호가 하나만 쓰이는 것은 할당 연산자이다.
```

## 조건문

* 조건 분기는 다른 상황에 따라 다른 코드가 실행되어야 한다는 개념을 말한다.
* 가장 흔히 쓰이는 조건은 if문인데 중괄호로 감싸진 한 코드 블록은 오직  
  소괄행에 쓰여진 조건이 참일때만 실행된다.

```c
    if (x > 0)
    {
        printf("positive\n");
    }
    else if (x < 0)
    {
        printf("negative\n");
    }
    else
    {
        printf("zero\n");
    }
```

### 1) else, else if

* 선택적으로 if문 뒤에 else 블록을 쓸수 있는데, if조건이 거짓일때 코드가 실행
* C에서는 한개 이상의 else if문을 쓸수 있는데, 조건을 더 추가하여 다른 코드  
  블록을 실행 시킬 수 있다.

![alt](/assets/images/post/computer science/CS50/1/36.png)

### 2) switch

* 조건식의 결과값에 따라 매칭되는 case의 코드를 실행시킨다.

```c
    switch (x)
    {
        case 1:
            printf("A\n");
                break;
        case 2:
            printf("B\n");
            break;
        default:
            printf("C\n");	
    }
```

### 3) 3항 연산자

* 식 하나를 받아서, 식이 참이면 : 기호 왼편에 값으로 계산 거짓이면 오른편의  
  값으로 계산된다.

```c
    int y = (x > 3) ? 2 : 1;
```

## 생각해보기

1. 간단한 조건문을 의사코드로 바꾸면 어떤 모습일까요?

```
    wake up in the morning
    if the time is go to school
        go to school
    else 
        go to tollet
```

2. 우리가 만드는 코드에서 의사 결정을 할 수 있다는 것이 왜 중요한가요?

```
    여러 경우들에 대비 할 수 있다.
```

## 실습

```c
    #include <stdio.h> 

    int main() 
    {
    //한 개의 변수를 선언하여 성인 나이를 저장합니다.
    int a=23;
    //조건문을 만들어 영화 요금을 출력해주세요.
    if(a>20){
            printf("성인요금: %d원",10000);	// 성인
    }
    else if(a>14){
            printf("청소년요금: %d원",7000);	// 청소년
    }
    else{
            printf("어린이요금: %d원",5000);	// 어린이
    }
    //성인이면 10000원,  청소년이면 7000원, 어린이는 5000원입니다.
    
    return 0; //main 함수를 종료합니다.
    }
```