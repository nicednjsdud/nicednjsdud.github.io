---
title: BackJoon Algorithm 16199 나이 계산하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나이 계산하기 (Java)
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-12 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/16199_1.png)
![alt](/assets/images/post/Algorithm/16199_2.png)



## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_16199 {
    public static void main(String[] args) throws IOException {
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token= new StringTokenizer(br.readLine());
        int year = Integer.parseInt(token.nextToken()); // 년 입력
        int month = Integer.parseInt(token.nextToken()); // 달 입력
        int day = Integer.parseInt(token.nextToken());  // 일 입력
        token= new StringTokenizer(br.readLine());
        int year2 = Integer.parseInt(token.nextToken()); // 년 입력
        int month2 = Integer.parseInt(token.nextToken()); // 달 입력
        int day2 = Integer.parseInt(token.nextToken());  // 일 입력

        // when
        int y3 = year2- year;           // 연 나이
        if(year<year2){                // 만나이
            if(month>month2){
                System.out.println(Math.abs(y3-1));
            }
            else if(month==month2){
                if(day>day2){
                    System.out.println(y3-1);
                }
                else {
                    System.out.println(y3);
                }
            }
            else{
                System.out.println(y3);
            }
        }
        else if(year==year2){
            System.out.println(y3);
        }
        // then
        System.out.println(y3+1);       // 세는나이
        System.out.println(y3);         // 연나이

    }
}

```


