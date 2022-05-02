---
title: CS50 15강 삽입 정렬
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- computer science
description: 삽입 정렬
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 삽입 정렬
last_modified_at: '2022-05-01 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---


![alt](/assets/images/post/computer science/CS50/1/0.jpg)

삽입 정렬
=========

## 삽입 정렬

* 자료를 정렬하는 알고리즘 중 하나이다.
* 자료를 여러 번 비교하거나 교환할 필요가 없는 방법이다.
* 자료가 정렬된 부분과 정렬되지 않은 부분으로 나눠진다.
* **정렬되지 않은 부분의 자료가 정렬된 부분의 자리로 삽입되는 형태의 정렬방법**

## 실행

* 삽입 정렬의 배열은 **정렬된 부분과 정렬되지 않은부분**, 두개의 부분으로 나누면서 작동한다.
* 만약 5,1,6,2,4,3 이라는 값을 삽입정렬을 이용하여 정렬을 할려면 다음과 같은  
  의사 코드로 작성할 수 있다.

```sql
    for each unsorted element, n, in the array

        determine where in the sorted porition of the 
        array to insert n

        shift sorted elements rightwards as necessary to
        make room for n

        insert n into sorted portion of the list

```

* 번역

```
    배열의 정렬되지 않은 각 요소 n에 대해

       n을 삽입할 배열의 정렬된 위치의 위치를 ​​결정합니다.
        
       필요에 따라 정렬된 요소를 오른쪽으로 이동하여
       n을 위한 공간을 마련합니다.

       목록의 정렬된 부분에 n을 삽입합니다.
```

![alt](/assets/images/post/computer science/CS50/1/20.png)


## 풀이

1. 프로그램이 실행되었을 떄, array라는 배열의 첫번째 자리 (5)는 이미   
  정렬된 부분이라고 간주한다.
2. 정렬되지 않은 부분의 맨 앞 자리인 1은 5보다 작기 때문에 5는 오른쪽  
  으로 이동하고 1이 첫번째 자리로 온다.
3. 다음으로 정렬되지 않은 부분의 6을 살펴본다.
4. 6은 5보다 크기 떄문에 이동할 필요x
5. 같은 방식으로 실행하면 전체 값이 모두 정렬된다.

## 정렬된 배열

* 삽입 정렬은 특정 실행 단계에서, 어떤 원소가 정렬된 배열 내에 자리를   
  찾았다고 해서 그것이 최종적인 제 자리라는 보장은 없다.
* 다음 단계가 진행되면서 다른 자료에 의해 위치가 바뀔수 있기 때문이다.
* 삽입 정렬은 자료의 양이 적을 때 성능이 우수하며 자료 대부분이 이미 정렬이  
  되어있는 경우 효율적이다. 
* 삽입정렬은 이미 정렬된 자료에 새로운 자료를 삽입해야 하는 경우가 발생하면,  
  정렬된 자료들이 자리를 이동해야 하므로 안정성이 낮다.

## 생각해보기

* 삽입 정렬이 다른 정렬 방법에 비해 갖는 장점과 단점은?

```
    장점 : 교환과 비교 횟수가 다른 정렬들(선택정렬, 버블정렬)보다 적다.
    단점 : 지정된 위치 변화가 잦을 가능성이 높아 안정성이 낮다.
```

* 삽입 정렬이 이전에 학습한 다른 정렬보다 선호되는 경우는 언제인가요?

```
    자료양이 적을때 교환과 비교횟수가 적어 효율성이 가장 좋을꺼같다.
    대신, 양이 많아질 수록 다른 정렬의 효율성보다 낮아진다.
```

