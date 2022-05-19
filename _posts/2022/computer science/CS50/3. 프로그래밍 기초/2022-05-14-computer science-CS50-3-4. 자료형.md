---
title: CS50 3-4강 자료형
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 자료형
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-14 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---


![alt](/assets/images/post/computer science/CS50/1/0.jpg)

Data Type
======

## 자료형

* C는 변수를 선언할 떄마다 변수의 자료형(Data Type)을 명시해줘야 하는  
  정적인 형식의 언어이다. 비교적 최근에 개발된 언어는 프로그램이  
  실행 시에 변수의 자료형을 유추하는 동적인 형식이다.

## C의 기본 자료형

* C의 기본자료형은 프로그래밍 언어 내에 설계된 자료형이다.  

### int형(정수형)

* int형(정수형)은 정수를 나타내는 자료형인데 이값은 양수,음수,0이 될수  
  있다. 
* int 형이 선언되면 컴퓨터는 변수를 저장하기 위한 공간으로 4byte  
  를 할당한다. 
* 4byte는 32bit이기 때문에 -2^31에서 2^31-1 까지 2^32(40억이 넘는 수)  
개의 사용할 수있는 정수가 있다는것을 의미

### unsinged int형

* C에는 자료형을 바꿔주기 위해 변수를 선언할 떄 int 앞에 추가로 작성  
  해주는 키워드인 **한정자**이다.
* 4byte 공간을 차지하면서도 음수를 사용 가능한 값의범위에 포함하지않는다.
* unsigned int형은 0부터 2^32-1까지 값을 사용할 수 있다.

### long형

* 더 많은 값을 저장할 수 있도록 더 많은 바이트 공간을 차지한다.
* long ling integer형은 4byte 대신 8byte의 저장공간을 사용하는 정수형  
  이다. -2^63에서 2^63-1까지의 수를 사용할 수 있다.

### float형

* 정수가 아닌수를 저장하는 형식이다.
* 2.8이나 3.14같은 소수를 저장하기 위해 4byte공간을 차지한다.

### double형

* 소수를 저장하지만 4바이트가 아닌 8byte의 공간을 차지한다.

### char형

* char형은 글자 하나를 표현하는데 a,b,c,~,z 등의 알파벳 뿐만아니라  
  !와 같은 특수문자, 그리고 '\n'과 같은 줄바꿈 기호도 나타낼수 있다. 
  char형은 항상 작은 따옴표를 이용하여('a')표현된다. 
* 1byte의 공간을 차지한다.

![alt](/assets/images/post/computer science/CS50/1/32.png)

## 생각해보기

1. 왜 C언어는 자료형에대해 융통성이 없을까요? 비교적 최근에 나온 언어와  
   연관하여 생각해보세요.

```
    C언어는 자료형마다 메모리크기를 다르게 해서 메모리를 최대한 아껴쓸수
    있지만 JavaScript나 python 등은 쫌더 범용적으로 만들어졌다. 
```

2. 어떤 경우 float형보다 double형을 사용하는 것이 좋을까요?

```
    큰 수를 표현할때 사용하는 것이 좋다. 
```
