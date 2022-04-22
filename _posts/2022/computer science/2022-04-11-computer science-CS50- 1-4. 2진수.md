---
title: CS50 4강 2진수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- computer science
description: 2진수
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs,binary
last_modified_at: '2022-04-11 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

2진수
=======

## 2진수란?

* 비트란 이진법의 최소단위로, 숫자 0,1로 신호를 나타내는 최소의 단위이다.
* 비트를 가지고 수학적 연산을 하기 위해, 컴퓨터는 0과 1만을 사용하는 2진수  
  라는 수 체계를 사용

## 수체계

* 우리가 사용하는 수 체계는 **10진수**이다.
* 10진수는 0부터 9까지 10개의 숫자를 이용하여 값을 표현한다.
* 10진수에서 각자리는 10의 거듭제곱을 나타낸다.

![alt](/assets/images/post/computer science/CS50/1/1.png)

* 컴퓨터는 전기적 신호 켜짐(1)과 꺼짐(0)을 이용하여 작동하기때문에 2진수 사용
* **2진수**는 0부터 1까지 2개의 숫자를 이용하여 값을 표현

![alt](/assets/images/post/computer science/CS50/1/2.png)

## 2진수에서 숫자를 세는 방법

* 10진수에서 숫자를 세는 방법과 비슷하지만 0과 1 두개의 수로만 제한된다.
* 2진수에서는 10진수 2를 사용할 수 없으므로 2를 나타내기 위해서는 또 다른  
  비트가 필요하고, **10진수 2는 2진수 10으로 나타냅니다.**
* 숫자 4를 나타내기에는 또비트가 모자랍니다. 10진수 4를 나타내기 위해  
  3번째 비트가 추가로 필요합니다. **10진수 4  = 2진수 100(4X1 + 2X0 + 1X0**
  )

![alt](/assets/images/post/computer science/CS50/1/3.png)

## 생각해보기

* 4개의 Binary Bulb가 있다면, 0,6,11 은 어떻게 표현 하나요?

```
    0 = 0000 , 6 = 0110 , 11 = 1011
```

* 2진법과 10진법만이 숫자를 표현 할 수 있는 유일한 방법 일까요?  
  3진법, 8진법, 16진법으로 50을 표현하세요

```
    3진법 50 = (3^3) + (3^2)*2 + 3 + 2 -> 1212
    8진법 50 = (8*6) + 1*2 -> 0062
    16진법 50 = (16*3) + 1*2 -> 0032
```
