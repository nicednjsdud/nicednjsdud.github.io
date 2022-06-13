---
published: true
title: BackJoon Algorithm 2445 별찍기-8 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-8
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-28 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2445.png)


## 풀이

* 총 (n*2-1) 의 줄이 출력되어야한다.
* 5번의 출력과 4번의 출력(역순) 두번에 나눠 출력하다. 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2445 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int temp=N;
        // when
        // 위의 별
        for(int i=1;i<=N;i++){      // 5번
            for(int j=0;j<i;j++){
                System.out.print("*");
            }
            for(int j=0;j<temp-1;j++){
                System.out.print("  ");
            }
            for(int j=0;j<i;j++){
                System.out.print("*");
            }
            System.out.println();
            temp--;
        }
        // 밑의 별
        temp=N;
        for(int i=1;i<N;i++){       // 4번
            for(int j=0;j<temp-1;j++){
                System.out.print("*");
            }
            for(int j=1;j<=i;j++){
                System.out.print("  ");
            }
            for(int j=0;j<temp-1;j++){
                System.out.print("*");
            }
            System.out.println();
            temp--;
        }

        // then
        br.close();
    }
}




```



