---
published: true
title: BackJoon Algorithm 10824 네 수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 네 수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10824.png)

## 풀이

- split() 함수를 사용하여 빈칸마다 잘라서 입력받는다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10824 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        // when
        String[] str = br.readLine().split(" ");    // 빈칸 자르기

        long num1 = Long.parseLong(str[0]+str[1]);
        long num2 = Long.parseLong(str[2]+str[3]);

        sb.append(num1+num2);

        // then
        br.close();
        System.out.println(sb);

    }
}


```
