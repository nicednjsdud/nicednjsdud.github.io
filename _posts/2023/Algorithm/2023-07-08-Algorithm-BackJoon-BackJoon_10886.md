---
published: true
title: BackJoon Algorithm 과자 10886 (Java)
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
last_modified_at: "2023-07-05 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10886.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10886 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        if (N % 2 != 0) {
           System.exit(0);
        }
        int notCute = 0;
        int cute = 0;

        for (int i = 0; i < N; i++) {
            int person = Integer.parseInt(br.readLine());
            if (person == 1) {
                cute++;
            } else if (person == 0) {
                notCute++;
            }
        }
        if (notCute > cute) {
            System.out.println("Junhee is not cute!");
        } else if (cute > notCute) {
            System.out.println("Junhee is cute!");
        }
        br.close();
    }
}



```
