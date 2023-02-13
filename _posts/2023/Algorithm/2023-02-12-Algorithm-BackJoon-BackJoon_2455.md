---
published: true
title: BackJoon Algorithm 지능형 기차 2455 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 피보나치 함수 1003
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-02-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2455.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2455 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int station_count = 4;
        int sum =0;
        int max = 0;
        for (int i = 0; i < station_count; i++) {
            st = new StringTokenizer(br.readLine());
            int get_off_count = Integer.parseInt(st.nextToken());
            int ride_count = Integer.parseInt(st.nextToken());

            sum -= get_off_count;
            sum += ride_count;
            if(sum >= max){
                max = sum;
            }
        }
        System.out.println(max);

    }
}

```