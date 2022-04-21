---
title: BackJoon Algorithm 9501 꿍의 우주여행
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 꿍의 우주여행
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-21 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9501.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* 시간당 최고속도이기때문에 거리 / 최고속도를 하면 가는데까지 걸리는 시간이 나온다.
* **(연료 * 위에 풀이)**를 하면 총가는데 쓰는 연료량이 나온다.
* 총가는데 쓰는 연료량 보다 현재 가지고 있는 연료량이 작으면 가지못한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_9501 {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // given
        int T = Integer.parseInt(br.readLine());      // 테스트 카운트 입력
        for(int i=1;i<=T;i++){
            StringTokenizer token = new StringTokenizer(br.readLine());
            int N = Integer.parseInt(token.nextToken());   // 우주선 갯수 입력
            double D = Double.parseDouble(token.nextToken()); // 거리입력
            int count =0;      // 체크 카운트
            for(int j=1;j<=N;j++){
                token = new StringTokenizer(br.readLine());
                double V = Double.parseDouble(token.nextToken()); // 최고속도
                double F = Double.parseDouble(token.nextToken()); // 연료량
                double C = Double.parseDouble(token.nextToken()); // 연료 소비율

                // when
                double arrive = D/V;   // 마지막 까지 가는데 걸리는 시간
                double check = F-(arrive*C);    // 갈수 있는지 없는지 체크
                if(check>=0){
                    count++;
                }
            }
            //then
            System.out.println(count);
            
        }
    }
}

```


