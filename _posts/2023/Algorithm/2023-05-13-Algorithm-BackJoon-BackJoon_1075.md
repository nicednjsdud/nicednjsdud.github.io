---
published: true
title: BackJoon Algorithm 1075 나누기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-05-13 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제
-
![alt](/assets/images/post/Algorithm/1075.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1075 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        long N = Long.parseLong(br.readLine());
        long F = Long.parseLong(br.readLine());

        long temp = (N / 100) * 100;

        while (true) {
            if (temp % F == 0) {
                long result = temp % 100;
                if (result < 10) System.out.println("0" + result);
                else System.out.println(result);
                return;
            }
            temp++;
        }
    }
}



```
