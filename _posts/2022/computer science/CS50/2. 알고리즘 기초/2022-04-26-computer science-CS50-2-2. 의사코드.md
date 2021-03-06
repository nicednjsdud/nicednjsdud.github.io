---
title: CS50 2-2강 의사코드
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 의사코드
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 의사코드
last_modified_at: '2022-04-26 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---


![alt](/assets/images/post/computer science/CS50/1/0.jpg)


의사코드
=========

## 의사코드

* 컴퓨터 프로그램은 프로그래밍 언어로 작성된다.
* 프로그래밍 언어는 일반적으로 기계가 알아들을 수 있도록 명령을 내리기 위해  
  사용되는 언어이다.
* 프로그래밍 언어는 특정한 문법에 의해 작성된 코드를 요구한다.
* 프로그래밍 언어보다 문법적 제약을 적게 받으므로 알고리즘 표현에 많이 사용
   
### 알고리즘 표현하는 방법 

* 자연어(Natural Language)
* 의사코드 (Pseudocode)
* 순서도 (flowchart)

## 의사코드 예시

* 방 안에 있는 사람의 수를 세기 위한 알고리즘을 만들어보자.
* 우리는 숫자 0부터 시작할 것이고 방안에 있는 각각의 사람을 셀 떄마다 1을 더함.

![alt](/assets/images/post/computer science/CS50/1/14.png)

* 1번 줄처럼 n이라는 이름을 부여하고 0 값을 넣어주는 것으로 시작한다.
* 이 과정은 **'할당'**이라고 불리는데, 이렇게 함으로써 우리가 만드는 코드 내  
  에서 값을 저장할 수 있는 공간n이 마련되고 거기에 0이라는 값이 초기값으로 들어감

```
    이제 방에 있는 각각의 사람을 위해 우리는 n 이 n+1이 되도록 다시 할당할 수 있다.
    그래서 한사람씩 늘어날 때마다 1씩 증가시켜 줄 수 있다.
```

* 알고리즘의 마지막에서 n은 방 안에 있는 사람 수 가 된다.

## 의사코드 예시2

* 더 복잡하지만 효율적인 의사 코드를 보여주기 위해 다른 방법을  
  사용할 수도 있습니다.
1. 방 안의 모든 사람을 일으켜 세우고 그들에게 숫자 1을 부여
2. 일어서 있는 다른 사람과 짝을짓고 그들이 갖고 있던 숫자를   
   더한 후 한 사람씩 앉는다.
3. 한사람이 남을 떄까지 반복하면 마지막 남은 사람에게 할당된  
   숫자는 방안의 총인원 수가 될것이다.

![alt](/assets/images/post/computer science/CS50/1/15.png)


* 프로그래밍 언어로 작성되지 않았는데도 이 알고리즘은 굉장히 정교
* 코드는 어떤 코드블록이 어떤 문장에 포함되는지 알 수 있도록  
  들여쓰기를 한다.

```
    ex) 4~9번 줄에 모두 들여쓰기가 되어 있는데, 이것은 3번줄에  
        작성된 '한 사람만 서있는 상태가 있을 떄까지' 그 아래줄들이
        반복되어야 한다는 뜻이다.
```

## 의사 코드의 요소

* 의사 코드를 작성하는 올바른 방법이란 없다.
* 의사 코드에는 값을 할당하는 개념이 종종 사용
* 의사 코드에는 반복문이나 조건문을 포함하기도 한다.
* 프로그래밍 언어로 작성된 프로그램에서도 중요한 개념이다.
* 프로그래밍 언어를 배운 후에도 의사 코드는 문법 걱정 없이 알고리즘을   
  단계별로 표현 할 수 있는 유용한 방법이며 프로그램의 논리를 이해하는데 효과적

## 생각해보기

1. 코드 작성법을 알고 있는데도 왜 의사 코드를 사용하나요? 의사코드 이점은?

```
    의사코드는 자연어 중에 프로그래밍과 가장 가까운 언어이다.
    컴퓨터 언어를 모르는 일반인들에게 설명 가능하며, 같이 사고할수 있다.
    보통 프로그램을 작성하기 전에 알고리즘의 모델을 대략적으로 모델링하기
     위해 의사코드를 작성합니다
```

2. 의사 코드는 늘 텍스트 기반으로 작성되어야 하나요? 문제해결 과정에서 의사코드  
를 다른 방식으로 사용할 수 있나요?

```
    그림을 그리거나 (마인드 맵) , 순서도 같은 것으로도 활용할 수 있다.
```
