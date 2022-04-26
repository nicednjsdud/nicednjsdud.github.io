---
title: BackJoon Algorithm 10539 수빈이와 수열
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 서버
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-26 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10539.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.

* 수열 A의 각 항의 합을 sum 라는 값에 저장한다.
 
```java
 B[i] = (sum + result) / (i+1)

 sum = sum + result

result = B[i] * (i+1) - sum; // 구하는 식
```


```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10539 {
    public static void main(String[] args) throws Exception{

        //given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());   // B의 길이 입력
        int B[]= new int[N];             // 수열 입력 받을 배열 생성

        // when
        StringTokenizer token = new StringTokenizer(br.readLine());
        for(int i=0;i<N;i++){
            B[i]= Integer.parseInt(token.nextToken());     // 수 입력
        }
        // then
        int sum=0;
        int result = 0;
        for(int i=0;i<N;i++){

            result = B[i] * (i+1) - sum;                   // A 수열 구하기
            sum +=result;
            System.out.print(result+" ");
        }
        br.close();

    }
}
```


