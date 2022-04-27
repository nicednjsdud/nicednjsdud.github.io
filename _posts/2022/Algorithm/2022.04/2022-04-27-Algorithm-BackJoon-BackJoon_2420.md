---
title: BackJoon Algorithm 2420 사파리월드
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 사파리월드
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-27 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2420.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.

* 절댓값을 구하는 문제이므로 Math.abs() 함수를 써본다
 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2420 {
    public static void main(String[] args) throws IOException {

        // when
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        long N = Integer.parseInt(token.nextToken());   // 유명도 N
        long M = Integer.parseInt(token.nextToken());   // 유명도 M

        long result;                                // 두 유명도의 차이

        result = Math.abs(N-M);                     // 절댓값 함수

        System.out.println(result);
    }
}


```


