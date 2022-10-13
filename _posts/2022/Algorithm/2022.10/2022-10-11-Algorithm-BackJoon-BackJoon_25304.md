---
title: BackJoon Algorithm 25304 영수증 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 영수증
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/25304_1.png)
![alt](/assets/images/post/Algorithm/25304_2.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_25304 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int total_price = Integer.parseInt(br.readLine());
        int total_count = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < total_count; i++) {
            StringTokenizer token = new StringTokenizer(br.readLine());
            int price = Integer.parseInt(token.nextToken());
            int count = Integer.parseInt(token.nextToken());
            total_price -= (price * count);
        }
        // then
        if( total_price == 0)
            System.out.println("Yes");
        else
            System.out.println("No");
        br.close();
    }
}




```
