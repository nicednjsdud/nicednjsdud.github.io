---
published: true
title: BackJoon Algorithm 알고리즘 수업 - 알고리즘의 수행 시간 3 24264 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 알고리즘 수업 - 알고리즘의 수행 시간 3
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-30 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/24264.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_24264 {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        Long n = Long.parseLong(br.readLine());
        System.out.println(n*n);
        System.out.println(2);

    }
}

```
