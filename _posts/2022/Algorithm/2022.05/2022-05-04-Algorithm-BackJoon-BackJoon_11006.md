---
title: BackJoon Algorithm 11006 남욱이의 닭장
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 남욱이의 닭장
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-04 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11006.png)



## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11006 {
    public static void main(String[] args) throws IOException {
        
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T =Integer.parseInt(br.readLine());     // 테스트 갯수입력
        // when
        for(int i=0;i<T;i++){
            StringTokenizer token = new StringTokenizer(br.readLine());
            int N =Integer.parseInt(token.nextToken()); 
                // 모든 닭의 다리수합
            int M =Integer.parseInt(token.nextToken());   // 닭의수
            int leg_sum = M*2;              // 닭은 다리가 2개
            int U = leg_sum - N;           // 잘린 다리수 찾기 and 닭의수
            int good =M-U;                               // 멀쩡한 닭

            // then
            System.out.print(U+" "+good);
            System.out.println();
        }
        
        
       
    }
}



```


