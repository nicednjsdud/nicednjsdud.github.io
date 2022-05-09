---
title: CS50 2-8강 합병 정렬
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 합병 정렬
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-06 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

합병 정렬
=========

## 합병 정렬

* 합병 정렬은 원소가 한개가 될 때까지 계속해서 반으로 나누다가 다시  
  합쳐나가며 정렬을 하는 방식이다.

## 실행

* 배열의 원소들이 반으로 나누어지는 과정과 정렬된 후 합쳐지는 과정으로   
  나누어져 있다.
* 우리가 만약 3,5,2,6,4,1 이라는 배열을 가지고 합병정렬을 이용하여 정렬해야  
  한다면 의사코드로 다음과 같이 작성할 수 있다.

```
    On input of n elements
        if n<2
                return
        else
                sort left half of elements
                sort right half of elements
                merge sorted halves
```

* 이 프로그램이 시작되면 6개의 원소를 가진 배열은 반으로 나뉘고,  
  원소가 1개가 될 떄까지 계속해서 나누어지게 된다.
* 모든 원소가 1개가 되었을 때, 다시 합치면서 정렬이 이루어지게 된다.
* step 4에서 5로 넘어가면서 3과 5의 크기를 비교하고 정렬된 채로 넘어가는  
  것처럼 나머지 나누어진 부분도 같은 방식으로 병합됨

![alt](/assets/images/post/computer science/CS50/1/22.png)

* 그림과 같이 step4를 중심으로 나우어지고(step2,step3) 합쳐지는과정  
  (step5,step6)이 역순으로 이루어져 있다는것을 알수 있다.
* 이렇게 나누어지고 합쳐지는 중간 단계의 배열을 임시로 저장하고 함수가  
  종료될 떄까지 기억하고 있어야 하기 때문에, 메모리의 필요한 공간이 늘어난다.

## 정렬된 배열

* 만약 8개의 원소가 있다면 3번 나누어질 것이다. 따라서 n개의 원소가 있을 떄  
  오나전히 나누어지기까지 호출되는 함수의 개수는 log n개라는 것을 알 수 있다.
* 합병 정렬은 병합하는 알고리즘에 포함된다.
* 합쳐지는 과정에서 각 원소들의 크기를 비교하기 때문에 n번의 비교 과정이 있다.
* 한번 나누어질 떄마다 n번의 비교 횟수가 추가되는 것이다. 
* 따라서 합병 정렬의 시간 복잡도는 O(n log n)이다.

## 생각해보기

* 합병 정렬은 확실히 더빠릅니다. 하지만 알고리즘이 어떻게 작동하는지 생각해보면,  
  그에 따른 단점이 떠오릅니다. 다른 정렬에는 없었던, 합병 정렬에서의 가장 큰  
  단점은 무엇일까요?

```
    - 다른 정렬에 비해 많은 메모리를 필요로 한다.
```

* 우리가 지금까지 다뤄본 알고리즘 중에 가장 마음에 드는 것은 무엇인가요?

```
  - 가장 마음에 드는 정렬은 버블 정렬이다. 모든면에서 중간 이상의 장점을 가지고 
    있다. 즉, 가장 무난하다.
```
