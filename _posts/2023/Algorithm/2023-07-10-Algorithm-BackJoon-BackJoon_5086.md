---
published: true
title: BackJoon Algorithm 배수와 약수 5086 (Java)
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
last_modified_at: "2023-07-10 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5086.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_5086 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        while (true) {
            st = new StringTokenizer(br.readLine());
            int first_num = Integer.parseInt(st.nextToken());
            int second_num = Integer.parseInt(st.nextToken());

            if (first_num == 0 && second_num == 0) {
                break;
            } else {
                if (first_num < second_num) {
                    if (second_num % first_num == 0) {
                        System.out.println("factor");
                    } else {
                        System.out.println("neither");
                    }
                } else if (first_num > second_num) {
                    if (first_num % second_num == 0) {
                        System.out.println("multiple");
                    }
                    else{
                        System.out.println("neither");
                    }
                }
            }
        }
        br.close();
    }
}



```
