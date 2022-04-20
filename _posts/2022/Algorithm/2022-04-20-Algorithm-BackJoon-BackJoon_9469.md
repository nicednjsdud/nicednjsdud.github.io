---
title: BackJoon Algorithm 9469 폰 노이만
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 폰 노이만
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9469.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* 각 A, B 기차가 1초마다 일정한 거리로 올때 파리의거리도 일정하게 증가
* 철로의 길이 = (A*B) * second 이기 때문에 
* 파리가 이동한 거리는 = F * second 이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_9469 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int P=Integer.parseInt(br.readLine());      // 테스트 개수

        for(int i=1;i<=P;i++){
            StringTokenizer token = new StringTokenizer(br.readLine());
            int count = Integer.parseInt(token.nextToken());        // 번호
            double N = Double.parseDouble(token.nextToken());       // 철로의 길이
            double A = Double.parseDouble(token.nextToken());       // A 기차 속도
            double B = Double.parseDouble(token.nextToken());       // B 기차 속도
            double F = Double.parseDouble(token.nextToken());       // 파리 속도

            double length = (N/(A+B))*F;

            System.out.printf("%d %.6f\n",count,length);
        }


    }
}


```


