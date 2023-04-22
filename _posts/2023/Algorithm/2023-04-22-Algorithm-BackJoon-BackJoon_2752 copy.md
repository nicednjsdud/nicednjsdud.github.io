---
published: true
title: BackJoon Algorithm 18406 럭키 스트레이트 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 18406 럭키 스트레이트 (Java)
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-22 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/18406.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_18406 {
    public static void main(String[] args) throws IOException {


        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();

        int length = str.length();
        int front_check = 0;
        int back_check = 0;
        for (int i = 0; i < length / 2; i++) {

            int first = Integer.parseInt(String.valueOf(str.charAt(i)));
            int second = Integer.parseInt(String.valueOf(str.charAt(i + (length / 2))));

            front_check += first;
            back_check += second;
        }

        if (front_check == back_check) {
            System.out.println("LUCKY");
        } else {
            System.out.println("READY");
        }
        br.close();

    }
}


```
