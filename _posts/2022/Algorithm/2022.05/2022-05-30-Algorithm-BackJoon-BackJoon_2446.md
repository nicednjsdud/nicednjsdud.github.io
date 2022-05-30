---
title: BackJoon Algorithm 2446 별찍기-9 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-9
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-30 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2446.png)


## 풀이

* 5줄과 4줄로 나눠서 출력하다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2446 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());        // 입력
        int Test_count = N*2-1;
        int temp =1;
        int star_temp =1;
        String str = " ";
        // when
        for(int i=1;i<=N;i++){              // 윗줄
            for(int j = 1;j<i;j++){
                System.out.print(str);
            }
            for(int j = star_temp;j<=Test_count;j++){
                System.out.print("*");
            }
            System.out.println();
            star_temp=star_temp+2;
        }
        star_temp=3;       // 밑에줄은 4개만 출력하면 되므로 별 1을 생략
        temp=2;
        for(int i=1;i<=N-1;i++){
            for(int j=temp;j<N;j++){
                System.out.print(str);
            }
            for(int j=1;j<=star_temp;j++){
                System.out.print("*");
            }
            System.out.println();
            star_temp=star_temp+2;
            temp++;
        }
        // then
        br.close();
    }
}


```



