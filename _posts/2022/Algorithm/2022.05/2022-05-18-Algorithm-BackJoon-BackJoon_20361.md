---
title: BackJoon Algorithm 20361 일우는 야바위꾼 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 일우는 야바위꾼
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/20361_1.png)
![alt](/assets/images/post/Algorithm/20361_2.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;

import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_20361 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int cup_count = Integer.parseInt(token.nextToken());       // 컵 갯수
        int first_position = Integer.parseInt(token.nextToken());  // 첫번째 공 위치
        int test_count = Integer.parseInt(token.nextToken());      // 테스트 카운트
        int temp =first_position;
        // when
        for(int i=0;i<test_count;i++){
            token = new StringTokenizer(br.readLine());
            int change_first = Integer.parseInt(token.nextToken()); // 첫번째 컵
            int change_last = Integer.parseInt(token.nextToken());  // 두번째 컵
            if(temp==change_first){
                temp=change_last;           // 공에위치랑 입력 받은 위치가 같다면
            }
            else if(temp==change_last){
                temp=change_first;
            }

        }
        // then
        System.out.println(temp);
        br.close();
    }
}
```


