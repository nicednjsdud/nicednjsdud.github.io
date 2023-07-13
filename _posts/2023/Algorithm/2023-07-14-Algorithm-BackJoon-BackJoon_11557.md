---
published: true
title: BackJoon Algorithm Yangjojang of The Year 11557 (Java)
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
last_modified_at: "2023-07-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11557.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Back_11557 {
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        StringBuilder sb = new StringBuilder();
        StringTokenizer st;

        int T = sc.nextInt();

        while (T > 0) {
            int N = sc.nextInt();
            String best = "";
            int count = 0;
            for (int i = 0; i < N; i++) {
                String S = sc.next();
                int L = sc.nextInt();
                if (L > count) {
                    count = L;
                    best = S;
                }
            }
            sb.append(best).append("\n");
            T--;
        }
        sc.close();
        System.out.println(sb);
    }
}


```
