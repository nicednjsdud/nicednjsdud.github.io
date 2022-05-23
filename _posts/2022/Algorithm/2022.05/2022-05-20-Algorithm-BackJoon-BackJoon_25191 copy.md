---
title: BackJoon Algorithm 25191 치킨댄스를 추는 곰곰이를 본 임스  (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 치킨댄스를 추는 곰곰이를 본 임스 
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

![alt](/assets/images/post/Algorithm/25191.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_25191 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int chicken =Integer.parseInt(br.readLine()); // 치킨 개수

        StringTokenizer token = new StringTokenizer(br.readLine());
        int coke = Integer.parseInt(token.nextToken());
        int beer = Integer.parseInt(token.nextToken());
        // when
        int sum = (coke/2)+beer;
        // then
        if(chicken>sum){
            System.out.println(sum);
        }
        else{
            System.out.println(chicken);
        }


        br.close();
    }
}


```
