---
title: BackJoon Algorithm 14910 오르막 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 오르막 (Java)
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-11 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/14910.png)



## 풀이


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_14910 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int Narr[]=new int[1000000];        // 정수 담을 배열
        int i=1;                            // 배열 카운트
        int badcount=0;
        StringTokenizer token = new StringTokenizer(br.readLine());
        Narr[0]=Integer.parseInt(token.nextToken());    // 첫번째 먼저담기
        // when
        while(token.hasMoreTokens()){
            Narr[i]=Integer.parseInt(token.nextToken());
            if(Narr[i]<Narr[i-1]){  
                badcount++;
            }
            i++;
        }
        // then
        if(badcount>0){
            System.out.println("Bad");
        }
        else{
            System.out.println("Good");
        }
        br.close();
    }
}




```


