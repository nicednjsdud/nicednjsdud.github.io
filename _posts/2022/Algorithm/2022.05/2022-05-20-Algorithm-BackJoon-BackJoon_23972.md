---
title: BackJoon Algorithm 23972 악마의 제안 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 악마의 제안
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/23972.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

// (가진돈-지불할돈)* 배수 = 가진돈
public class Back_23972 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        long K = Long.parseLong(token.nextToken());        // 제안한 K
        long N = Long.parseLong(token.nextToken());        // 제안한 N
        long x=(K/2)*N;
        // when
        long result =0;
        if(N!=1L){
            result=(K*N)/(N-1L);

            if((K*N)%(N-1L)!=0L){
                result += 1L;
            }
        }
        else{
            result= -1L;
        }
        //then
        System.out.println(result);
        br.close();
    }
}


```
