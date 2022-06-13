---
published: true
title: BackJoon Algorithm 2440 별찍기-4 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-4
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-26 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2441.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2441 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int star_count = Integer.parseInt(br.readLine()); // 별의 개수
        int k=star_count;                                       
        int temp = 0;                                // 빈칸 변수
        // when
        for(int i=0;i<star_count;i++){
            for(int l=0;l<temp;l++){
                System.out.print(" ");                 // 빈칸
            }
            for(int j=k;j>0;j--){
                System.out.print("*");                 // 별
            }
            System.out.println();
            k--;
            temp++;
        }
        // then
        br.close();
    }
}


```



