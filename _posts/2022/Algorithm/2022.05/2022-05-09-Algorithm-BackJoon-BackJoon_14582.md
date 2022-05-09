---
title: BackJoon Algorithm 14582 오늘도 졌다
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 오늘도 졌다
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-09 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/14582.png)



## 풀이

* 9회말 까지 울림이 한번이라도 이기고 있다면 역전패이기 때문에 Yes출력하다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_14582 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int arr[]=new int[9];                   // 울림 제미니스
        int arr2[]=new int[9];                  // 스타트링크 걸리버스
        // when
        StringTokenizer token = new StringTokenizer(br.readLine());
        for(int i=0;i<9;i++){
            arr[i]=Integer.parseInt(token.nextToken()); // 울림 입력
        }
        token = new StringTokenizer(br.readLine());
        for(int i=0;i<9;i++){
            arr2[i]=Integer.parseInt(token.nextToken()); // 스타트링크 입력
        }
        int sum=0;                                      // 울림 총점
        int sum2=0;                                     // 스타트링크 총점
        for(int i=0;i<9;i++){
            
            sum=arr[i]+sum;
            if(sum>sum2){               // 울림이 한번이라도 이기고 있다면
                System.out.println("Yes");
                return;
            }
            sum2=arr2[i]+sum2;
        }
        System.out.println("No");
        br.close();
    }
}


```


