---
title: BackJoon Algorithm 23448 스트릿 코딩 파이터 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 스트릿 코딩 파이터
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-19 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/23448_1.png)
![alt](/assets/images/post/Algorithm/23448_2.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_23348 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int one_hand = Integer.parseInt(token.nextToken()); // 한손코딩
        int no_look =Integer.parseInt(token.nextToken());   // 노룩코딩
        int phone = Integer.parseInt(token.nextToken());    // 폰코딩
        int team_count = Integer.parseInt(br.readLine());   // 동아리수
        int temp=0;
        // when
        for(int i=0;i<team_count;i++){
            int sum=0;                                      // 총점 비교
            for(int j=0;j<3;j++){
                token= new StringTokenizer(br.readLine());
                int first = Integer.parseInt(token.nextToken());
                int second = Integer.parseInt(token.nextToken());
                int third = Integer.parseInt(token.nextToken());
                sum += (first*one_hand)+(second*no_look)+(third*phone); 
                // 동아리마다 총점계산
            }
            if(sum>=temp){
                temp = sum;                    // 변수에 총점담기
            }
        }
        //then
        System.out.println(temp);
        br.close();
    }
}

```
