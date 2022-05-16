---
title: CS50 2-9강 이진 탐색
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 이진 탐색
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-08 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

이진 탐색
=========

## 이진 탐색

* 선형 탐색보다 더 빠른 알고리즘으로 이진 탐색이 있다.
* 이진 탐색은 자료를 절반으로 나눈 후 찾는 값이 어느 쪽에 있는지 파악해  
  탐색의 범위를 반으로 줄여나가는 탐색 알고리즘이다.

## 효율성과 비효율성

* 배열은 정렬하는 데는 버블 정렬, 삽입정렬, 선택정렬 등 다양한 방법이  
  있다.
* 이 정렬 방법은 사실 이진 탐색을 구현하는 데 유용하다.
* 이진 탐색의 기본은 정렬된 배열을 만들 수 있다는데 가정을 두고 있다.

### 배열에서 50을 찾아보자

![alt](/assets/images/post/computer science/CS50/1/23.png)

```c
    set minimum = 0 and maximun = n - 1
    find middle of array
    if k is less than arry[middle]
        set maximum to middle - 1
        go to line 2
    else if k is greater than array[middle]
        set minimun to middle + 1
        go to line 2
    else if k is equal to array[middle]
        you found k in the array!
    else
        k is not in the array
```

1. 먼저 최소값을 배열의 첫 번째 값(1), 그리고 최대값을 배열의 마지막  
  값(63)으로 정합니다.
2. 그리고 중간값을 계산한다. 중간값은 네번쨰 값(29)가 될수도 있고,  
  다섯 번째 값(38)이 될수도 있다. 어떤 값을 정하던 알고리즘은 일관적  
  이기 때문에 상관은 없다.
3. 29를 중간값으로 사용했을 떄, 50은 29보다 크기 때문에 왼편에 있는 값  
  은 살펴 볼 필요가 없다.
4. 최소값은 중간값 오른편에 있는 38로 정해지고, 최대값은 그대로 남겨둔  
   후 같은 방식으로 진행한다.

## 이진 탐색 VS 선형 탐색

* 우리가 어떤 부분을 좋게 만들면 반드시 다른 부분에서 비용이 발생한다는  
  것은 컴퓨터 과학에서는 일반적인 사실이다.
* 이진 탐색은 일반적으로 선형탐색보다 탐색 속도가 짧지만, 배열을 정리  
  하는 시간이 추가된다.
* 선형적으로 배열을 탐색하는 것이 배열을 정렬한 후 이진 탐색을 사용하는  
  것보다 빠르게 보이기도하고, 사실 어떤 상황에서는 이것이 사실이기도 하다.
* 하지만 배열을 여러번 탐색할 계획이 있다면 이진 탐색이 유용하게 사용된다.
* 찾고자 하는 값이 배열에 없는 경우 선형 탐색은 배열의 길이가 얼마든   
  상관없이 배열 전체를 훑어보아야 배열 안에 찾고자 하는 값이 없다는 것을  
  알 수 있다.
* 이에반해 이진 탐색에서는 더 효율적으로 사용할 수 있다.
* 의사코드를 수행해보면, 찾고자 하는 값이 최소값보다 작너나 최대값보다  
  크다면 해당 원소가 배열안에 없다는 것을 알 수 있다.

## 생각해보기

* 어떤 조건일때 이진 탐색을 하는것이 선형 탐색을 하는것보다 효율적인가요?

```
    배열을 여러번 탐색할 계획이 있다면 유용하게 사용된다.
```

* 64개,4096개,4294967296개의 데이터에 이진 탐색을 수행하는데   
  최대 몇 번의 과정을 거쳐야 할까요?

```
    2^6 6번 2^12 12번 2^32 32번
```
