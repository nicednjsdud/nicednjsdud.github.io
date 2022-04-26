---
title: BackJoon Algorithm 10419 지각
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 지각
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-26 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10419.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.

* 지각한 시간을 while문으로 조건에 만족할때 까지 돌린다.
 

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Back_10419 {
    public static void main(String[] args) throws Exception{

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        // given
        int T = Integer.parseInt(br.readLine());    // 경우의 수

        int d = 0;                                  // 수업시간 입력
        // then
        for(int i=0;i<T;i++){
            d = Integer.parseInt(br.readLine());
            int t=1;                                    // 최대시간

            while((t*t)+t <= d){       // 입력 + 지각 <= 최대시간
                t++;
            }
            System.out.println(t-1);
        }

    }
}

```


