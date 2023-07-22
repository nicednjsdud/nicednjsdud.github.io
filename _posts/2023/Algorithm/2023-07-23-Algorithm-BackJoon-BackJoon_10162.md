---
published: true
title: BackJoon Algorithm 전자레인지 10162 (Java)
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
last_modified_at: "2023-07-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10162.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10162 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        int first = 0;
        int second = 0;
        int third = 0;
        if(T % 10 == 0){
            while(true){
                if(T < 300){
                    break;
                }
                T = T - 300;
                first++;
            }
            while(true){
                if(T < 60){
                    break;
                }
                T = T - 60;
                second++;
            }
            third = T / 10;

            System.out.println(first + " " + second + " " + third);
        }
        else{
            System.out.println(-1);
        }
        br.close();
    }
}



```
