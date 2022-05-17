---
title: BackJoon Algorithm 20299 3대측정 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 3대측정
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-17 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/20299_1.png)
![alt](/assets/images/post/Algorithm/20299_2.png)

## 풀이

* ArrayList()를 쓰면 시간 초과가 나온다.
* StringBuilder 메서드를 사용하다.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;


public class Back_20299 {
    public static void main(String[] args) throws Exception{

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        int team_count =Integer.parseInt(token.nextToken());    // 팀의수
        int rating_sum =Integer.parseInt(token.nextToken());    // 레이팅 합
        int private_rating = Integer.parseInt(token.nextToken());   // 개인 레이팅조건
        int count =0;   // 클럽가능한 팀의 수
        // when

        for(int i=0;i<team_count;i++){
            token = new StringTokenizer(br.readLine());
            int t1 =Integer.parseInt(token.nextToken());    // 팀원1
            int t2 =Integer.parseInt(token.nextToken());    // 팀원2
            int t3 =Integer.parseInt(token.nextToken());    // 팀원3
        // then
            if(rating_sum<=(t1+t2+t3)){
                if(private_rating<=t1&&private_rating<=t2&&private_rating<=t3){
                    count ++;
                    sb.append(t1+" ");
                    sb.append(t2+" ");
                    sb.append(t3+" ");// 리스트에 담기
                }
            }

        }
        System.out.println(count);
        System.out.println(sb);
        br.close();
    }

}



```


