---
published: true
title: BackJoon Algorithm 2908 상수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: OX퀴즈
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-15 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2908.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2908 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int first_num = Integer.parseInt(st.nextToken());
        int next_num = Integer.parseInt(st.nextToken());
        // when
        first_num = (first_num % 10) * 100 + ((first_num / 10) % 10) * 10 + (first_num / 100);
        next_num = (next_num % 10) * 100 + ((next_num / 10) % 10) * 10 + (next_num / 100);

        if (first_num > next_num)
            System.out.println(first_num);
        else
            System.out.println(next_num);

        // then
        br.close();
    }
}


```
