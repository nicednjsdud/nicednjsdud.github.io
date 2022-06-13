---
published: true
title: BackJoon Algorithm 10991 별찍기-16 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-16
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-29 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10991.png)


## 풀이

* 홀수이면 *을 먼저출력 짝수이면 빈칸을 먼저출력하다. 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10991 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());   // 입력
        int temp=1;                           // 공백을 한칸씩 지워준다.
        // when
        for(int i=1;i<=N;i++){
          for(int j=temp;j<=N-1;j++){          // 처음 빈칸측정
              System.out.print(" ");
          }

          for(int j=1;j<=((2*i)-1);j++){
              if(j%2 == 1){         // 홀수이면
                  System.out.print("*");
              }
              else{
                  System.out.print(" "); //짝수이면
              }
          }
          System.out.println();
          temp++;
        }
        // then
        br.close();
    }
}






```



