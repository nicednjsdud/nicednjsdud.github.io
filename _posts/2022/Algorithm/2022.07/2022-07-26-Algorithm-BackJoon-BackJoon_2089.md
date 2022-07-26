---
published: true
title: BackJoon Algorithm 2089 -2진수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: -2진수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2089.png)

## 풀이

- 문제에 주어진 - 13 은 (-2 \* 7) + 1과 같다
- 나머지는 항상 양수이므로 올림 처리를 한다 (홀수일 경우) Math.ceil()함수 이용

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2089 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int n = Integer.parseInt(br.readLine());
        // when
        if (n == 0) {
            System.out.println(0);
        } else {
            while (n != 1) {
                sb.append(Math.abs(n % -2));
                n = (int) Math.ceil((double) n / (-2));
            }
            sb.append(n);
        }

        // then
        br.close();
        System.out.println(sb.reverse());
    }
}
```
