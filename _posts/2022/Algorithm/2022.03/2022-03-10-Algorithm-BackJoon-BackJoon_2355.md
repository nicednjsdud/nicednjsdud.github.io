---
title: BackJoon Algorithm 2355 시그마
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 시그마
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-10 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2355.png)




## 풀이

* 출력시간이 0.25초 제한이므로 for문은 돌리면 stackoverflow가 나온다.
* int형으로 받기에는 출력값이 그 이상이여서 long 타입으로 받는다.


```java

import java.util.Scanner;

public class Back_2355 {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        // 1. 두 자연수 입력받기
        long A = sc.nextLong();
        long B = sc.nextLong();
        // 1.1 모든수의합
        long sum=0;

        // 2. A, B중 더큰수 찾기

        // 2.1 A가 B보다 크거나같을때
        if(A>=B){

           sum= (A+B)*(A-B+1) / 2;
        }
        // 2.2 B가 A보다 클때
        else if(A<B){

           sum= (B+A)*(B-A+1) / 2;

        }
      
        
        System.out.println(sum);
        sc.close();

    }
}
```


