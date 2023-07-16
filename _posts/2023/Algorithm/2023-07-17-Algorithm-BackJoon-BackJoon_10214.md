---
published: true
title: BackJoon Algorithm baseball 10214 (Java)
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
last_modified_at: "2023-07-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10214.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10214 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine());
        StringTokenizer st;

        while (T > 0) {

            int yCount = 0;
            int kCount = 0;

            for (int i = 0; i < 9; i++) {
                st = new StringTokenizer(br.readLine());
                yCount += Integer.parseInt(st.nextToken());
                kCount += Integer.parseInt(st.nextToken());
            }

            if (yCount > kCount) {
                System.out.println("Yonsei");
            } else if (yCount < kCount) {
                System.out.println("Korea");
            }
            else{
                System.out.println("Draw");
            }
            T--;
        }
        br.close();
    }
}




```
