---
title: BackJoon Algorithm 19572 가뭄small (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 가뭄small
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-16 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/19572.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_19572 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());

        int d1 = Integer.parseInt(token.nextToken());
        int d2 = Integer.parseInt(token.nextToken());
        int d3 = Integer.parseInt(token.nextToken());

        double a = (d1+d2-d3)/2.0;
        double b = (d1-d2+d3)/2.0;
        double c = (-d1+d2+d3)/2.0;

        if( a<=0 || b<=0|| c<=0){
            System.out.println(-1);
        }
        else{
            System.out.println(1);
            System.out.printf("%.1f %.1f %.1f",a,b,c);
        }
        br.close();
    }
}


```


