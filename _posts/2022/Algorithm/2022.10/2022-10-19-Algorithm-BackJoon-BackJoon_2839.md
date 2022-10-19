---
published: true
title: BackJoon Algorithm 2839 설탕 배달 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 설탕 배달
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-19 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2839.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2839 {

    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int count = 0;
        // when

        // 4나 7은 떨어지지 않음.
        if (N == 4 || N == 7) {
            count = -1;
        }
        // 5로 나누어 떨어질때
        else if ((N % 5 == 0)) {
            count = N / 5;
        }
        // 나머지가 1 혹은 3일때 ex) 6 , 11 || 8 , 13
        else if ((N % 5) == 1 || (N % 5) == 3) {
            count = (N / 5) + 1;

            // 나머지가 2 혹은 4일때 ex) 12 , 17 || 9 , 14
        } else if ((N % 5) == 2 || (N % 5) == 4) {

            count = (N / 5) + 2;
        }

        // then
        System.out.println(count);
        br.close();
    }
}


```
