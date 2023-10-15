---
published: true
title: BackJoon Algorithm 아름다운 수 2774 (Java)
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
last_modified_at: "2023-10-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2774.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2774 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            String str = br.readLine();
            boolean[] check = new boolean[11];
            for (int j = 0; j < check.length; j++) {
                check[j] = false;
            }
            int count = 0;
            for (int j = 0; j < str.length(); j++) {
                int num = Integer.parseInt(String.valueOf(str.charAt(j)));
                if(check[num] == false){
                    check[num] = true;
                    count++;
                }
            }
            System.out.println(count);
        }
        br.close();
    }
}

```
