---
title: BackJoon Algorithm 14645 와이버스 부릉부릉
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 와이버스 부릉부릉
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-10 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/14645.png)



## 풀이



```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_14645 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(token.nextToken());        
                                        // 종착역 제외한 정거장의 수
        int K = Integer.parseInt(token.nextToken()); 
                                     // 출발역에서 탑승하는 사람 수
        // when
        
        for(int i=0;i<N;i++){
            token= new StringTokenizer(br.readLine());
            int A = Integer.parseInt(token.nextToken());    
            // 탑승하는 인원 A
            int B = Integer.parseInt(token.nextToken());    
            // 탑승하는 인원 B
        }
        // then
        System.out.println("비와이");
    }
}



```


