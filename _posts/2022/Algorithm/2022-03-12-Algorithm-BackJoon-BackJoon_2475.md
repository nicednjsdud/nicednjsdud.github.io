---
title: BackJoon Algorithm 2475 검증수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 검증수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-12 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2475.png)




## 풀이


```java

import java.util.Scanner;

public class Back_2475 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 1. 입력
        int arr[]= new int[5];
        int sum=0;
        int result=0;

        // 1.1 배열에 입력 넣기
        for(int i=0;i<arr.length;i++){
            arr[i] = sc.nextInt();
        }
        sc.close();
        // 2.1 각 배열수마다 제곱하여 합하기
        for(int i=0;i<arr.length;i++){
            sum += (arr[i] * arr[i]);
        }
        result= sum%10;

        System.out.println(result);


    }
}
```


