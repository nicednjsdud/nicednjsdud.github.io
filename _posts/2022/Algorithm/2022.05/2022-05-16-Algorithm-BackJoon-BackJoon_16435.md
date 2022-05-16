---
title: BackJoon Algorithm 16435 스네이크버드 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 스네이크버드 (Java)
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

![alt](/assets/images/post/Algorithm/16435.png)

## 풀이

* 배열로 대입받아 오름차순으로 정렬후 앞에서부터 하나씩 대입해본다.
* 만약 중간에 멈추면 더이상 먹을수 없는것이기에 그대로 출력하다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_16435 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int fruit_count = Integer.parseInt(token.nextToken());// 과일의 개수
        int snake_length = Integer.parseInt(token.nextToken());     // 스네이크 초기길이
        int height[]= new int[fruit_count];           // 과일의 높이
        token = new StringTokenizer(br.readLine());
        for(int i=0;i<fruit_count;i++){
            height[i]= Integer.parseInt(token.nextToken());//배열에과일높이 대입
        }
        Arrays.sort(height);                          // 오름차순 정렬
        for(int i=0;i<fruit_count;i++){
            if(height[i]<=snake_length){
                snake_length++;
            }
        }
        // then
        System.out.println(snake_length);
        br.close();
    }
}

```


