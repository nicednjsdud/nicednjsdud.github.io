---
title: BackJoon Algorithm 2558 A+B-2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: A+B-2 
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-23 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2558.png)


## 풀이

```java
import java.util.Scanner;

public class Back_2558 {
    public static void main(String[] args) {

        // given
        Scanner sc = new Scanner(System.in);
        int A = sc.nextInt();   // A입력
        int B = sc.nextInt();   // B입력
        // then
        System.out.println(A+B);
        sc.close();
    }
}



```
