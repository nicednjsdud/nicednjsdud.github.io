---
title: CS50 3-5강 연산자
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 연산자
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

연산자
======

## 연산자

* C에서는 덧셈,뺄셈,곱셈 그리고 나눗셈 같은 기본 산술 연산을 수행하는 연산자  
  를 사용할 수 있을 뿐만 아니라 나눗셈을 하거나 또는 변수의 값을 갱신햇을 때  
  생기는 나머지 값을 찾아주는 또 다른 함수도 사용할 수 있다.

## 산술 연산자

![alt](/assets/images/post/computer science/CS50/1/33.png)

* C의 산술 연산자는 수학적 기능을 한다.
* int형 변수와 나눗셈을 같이 수행해줄 때, 정수는 정수가 아닌 변수를 저장하지  
  못한다는 것을 알고 있는 것이 중요하다.
* 소수점 이하의 정확한 답을 원할 경우 형변환을 해줘야 한다.

### 나머지 연산자(%)

* 나머지 연산자는 연산자 왼편의 수가 오른편의 수로 나눠질 때 발생하는  
  나머지를 구해주는것이다.
* 13을 3으로 나누었을 때의 나머지 값인 1이 f에 저장하는 것을 보여주는 6 행은  
  나머지 연산자를 어떻게 사용 할 수 있는지 보여준다.
* 나머지 연산자는 정수형 끼리만 사용할수 있다.

## 할당 연산자

![alt](/assets/images/post/computer science/CS50/1/34.png)

* 변수의 값을 갱신하는 연산자이다.
* 할당 받는 변수는 등호의 왼쪽에 위치한다.

### 증감 연산자

* e++ 같은 문장은 e값을 1만큼 증가 시켜준다. 이와같은 연산자를 증감연산자 라고함.

## 생각해보기

1. C의 연산자를 수학의 연산자와 어떻게 비교할수 있나요?

```
  산술연산자는 수학적 기능을 한다. /은 나누기 %은 나머지이다.
```

2. ++,--,+= 그리고 *=와 같은 약식으로 표현한 연산들은 무엇을 나타낼까요?

```
  ++,-- 증감연산자
  +=,*= 할당연산자
```

## 실습

```c++
int main() 
{
  //이 아래부터 코드를 작성합니다.
  //두 개의 변수를 선언하고, 순서대로 250과 50을 저장합니다.
    int a = 250;
      int b = 50;
  //두 수로 사칙연산을 수행하여 출력합니다. 
  //더하기, 빼기, 곱하기, 나누기 순으로 수행합니다.
  //각 연산은 줄내림 하여 구분합니다.
   printf("%d\n",a+b);  // 300
   printf("%d\n",a-b);  // 200
   printf("%d\n",a*b);  // 12500
   printf("%d\n",a/b);  // 5
   
  
  return 0; //main 함수를 종료합니다.
}
```

