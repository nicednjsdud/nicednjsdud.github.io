---
published: true
title: BackJoon Algorithm 2440 별찍기-5 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-5
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-27 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2442.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2442 {
    public static void main(String[] args) throws IOException {


        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int star_count = Integer.parseInt(br.readLine());
        // when
        for(int i=1;i<=star_count;i++){
            for(int j=i;j<star_count;j++){
                System.out.print(" ");
            }
            for(int j=0;j<(i*2)-1;j++){
                System.out.print("*");
            }
            System.out.println();
        }
        // then
        br.close();
    }
}



```



