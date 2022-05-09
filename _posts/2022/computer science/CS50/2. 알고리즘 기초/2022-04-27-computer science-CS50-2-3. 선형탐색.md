---
title: CS50 2-3강 선형 탐색
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 선형 탐색
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 선형 탐색
last_modified_at: '2022-04-27 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

선형 탐색
==========

## 선형 탐색

* 선형탐색은 원하는 원소가 발견될 떄 까지 처음부터 마지막 자료까지 차례대로 탐색
* 찾고자 하는 자료를 찾을 때 까지 모든 자료를 확인해야 한다.

![alt](/assets/images/post/computer science/CS50/1/16.png)

## 효율성 그리고 비효율성

* 선형탐색 알고리즘은 정확하지만 아주 효율적이지 못한 방법이다.
* 리스트의 길이가 n이라고 했을 떄 , 최악의 경우 리스트의 모든 원소를 확인해야  
  하므로 n번만큼 실행된다.

```
    - 최악의 상황은 찾고자 하는 자료가 맨 마지막에 있거나 리스트 안에 없는 경우
    - 만약 100만개의 원소가 있는 리스트라고 가정해본다면 효율성이 매우 떨어짐.

    - 최선의 상황은 처음 시도했을 떄 찾고자 하는 값이 있는 경우
```

* 평균적으로 선형 탐색이 최악의 상황에서 종료되는 거셍 가깝다고 가정할 수 있다.
* **자료가 정렬되어 있지 않거나 그 어떤 정보도 없어 하나씩 찾아야 하는 경우에 유용**

```
  이러한경우 무작위로 탐색하는것보다 순서대로 탐색하는 것이 더효율적
```

## 생각해보기

* 언제 선형 탐색을 사용하는것이 유용할까요? 유용하지 않은 경우는 어떤 경우?

```
    - 순서가 정렬이 되어있지 않을때
    - 자료 범위가 방대한 경우는 유용 x
```
