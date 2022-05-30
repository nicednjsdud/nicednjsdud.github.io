---
title: BackJoon Algorithm 10992 별찍기-17 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 별찍기-17
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

![alt](/assets/images/post/Algorithm/10992.png)


## 풀이

* 마지막 줄은 따로 출력하면 편하게 할수 있다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10992 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());        // 입력
        int temp=1;
        // when
        for(int i=1;i<=N-1;i++){
            for(int j=temp;j<=N-1;j++){
                System.out.print(" ");
            }

            for(int j=1;j<=((2*i)-1);j++){
                if(j%2 == 1 ){
                    if(j==1||j==(2*i)-1) {          // 중간에 별 뺴기,맨앞과 맨뒤별만 출력
                        System.out.print("*");
                    }
                    else{
                        System.out.print(" ");
                    }
                }
                else{
                    System.out.print(" ");
                }
            }
            System.out.println();
            temp++;
        }
        for(int i=0;i<(N*2)-1;i++){             // 맨밑줄은 따로출력
            System.out.print("*");
        }
        // then
        br.close();
    }
}

```



