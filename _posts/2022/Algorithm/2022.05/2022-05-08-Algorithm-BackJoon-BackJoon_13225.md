---
title: BackJoon Algorithm 13225 Divisors
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: Divisors
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-08 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/13225.png)



## 풀이

* 영어문제라서 당황할 필요가없다. 
* 테스트 갯수가 주어지고 정수마다 공약수를 구하는 문제이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_13225 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int C =Integer.parseInt(br.readLine());         // 테스트 갯수

        // when
        for(int i=1;i<=C;i++){
            int n =Integer.parseInt(br.readLine());     // 수입력
            int count=0;                                // 갯수세기
            for(int j=1;j<=n;j++){                       // 공약수 찾기
                if(n%j==0){
                    count++;
                }
            }
            // then
            System.out.println(n+" "+count);

        }
        br.close();


    }
}

```


