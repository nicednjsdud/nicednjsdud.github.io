---
title: BackJoon Algorithm 3046 R2
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: R2
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-28 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/3046.png)



## 풀이


```java
import java.util.Scanner;

public class Back_3046 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        // 입력
        int R1= sc.nextInt();
        int S=sc.nextInt();
        int R2=(S*2)-R1;

        System.out.println(R2);
    }
}


```

