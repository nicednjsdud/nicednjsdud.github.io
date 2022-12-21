---
published: true
title: BackJoon Algorithm 오각형, 오각형, 오각형… 1964 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 균형잡힌 세상
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-12-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1964.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1964 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        long result = 5;
        long dot = 7;
        if (N == 1) {
            System.out.println(result % 45678);
        } else {
            // 1 개 5
            // 2 개 5 + ( 5 + 2 )    2번째까지는 2개씩 늘어나지만 3번째부터는 3개씩 늘어남
            // 3 개 5 + ( 5 + 2 ) + ( 7 + 3 )
            // 4 개 5 + ( 5 + 2 ) + ( 7 + 3 ) + ( 10 + 3 )
            for (int i = 2; i <= N; i++) {
                result += dot;
                dot += 3;
            }
            System.out.println(result % 45678);
        }
        br.close();
    }
}
```
