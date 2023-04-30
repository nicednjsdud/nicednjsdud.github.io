---
published: true
title: BackJoon Algorithm 10093 숫자 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 10816 숫자 카드2
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10093.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10093 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        long A = Long.parseLong(st.nextToken());
        long B = Long.parseLong(st.nextToken());

        if (A > B) {
            System.out.println(A - B - 1);
            for (long i = B + 1; i < A; i++) {
                sb.append(i).append(" ");

            }
            System.out.println(sb);
        } else if (A < B) {
            System.out.println(B - A - 1);
            for (long i = A + 1; i < B; i++) {
                sb.append(i).append(" ");

            }
            System.out.println(sb);
        } else {
            System.out.println(0);
        }
        br.close();
    }
}




```
