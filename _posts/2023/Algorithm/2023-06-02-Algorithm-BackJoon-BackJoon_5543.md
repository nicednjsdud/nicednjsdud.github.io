---
published: true
title: BackJoon Algorithm 5543 상근날드 (Java)
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
last_modified_at: "2023-06-02 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5543.png)

## 풀이

```java
iimport java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_5543 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int hamburger[] = new int[3];
        int drink[] = new int[2];

        for (int i = 0; i < 3; i++) {
            hamburger[i] = Integer.parseInt(br.readLine());
        }

        for (int i = 0; i < 2; i++) {
            drink[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(hamburger);
        Arrays.sort(drink);

        System.out.println(hamburger[0] + drink[0] - 50);
        br.close();
    }
}


```
