---
title: BackJoon Algorithm 15734 명장 남정훈 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 명장 남정훈 (Java)
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-11 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/15734.png)



## 풀이

* 간단한 사칙연산 문제이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_15734 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());

        int L = Integer.parseInt(token.nextToken());     // 왼발잡이
        int R = Integer.parseInt(token.nextToken());     // 오른발 잡이
        int A = Integer.parseInt(token.nextToken());     // 양발 잡이
        // when
        int sum = L + R + A;
        int temp = A- Math.abs(L-R);
        // then
    System.out.println(temp >= 0 ? sum -(temp % 2):sum - Math.abs(temp));
    }
}
```


