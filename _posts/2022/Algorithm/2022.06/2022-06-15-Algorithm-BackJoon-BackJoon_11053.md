---
published: true
title: BackJoon Algorithm 11053 가장 긴 증가하는 부분 수열 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 가장 긴 증가하는 부분 수열
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-15 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11053.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11053 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n= Integer.parseInt(br.readLine());
        int arr[]=new int[n];       // 수열 A(i)
        int seq[]=new int[n];       // 수열 배열 생성
        StringTokenizer token=new StringTokenizer(br.readLine());
        // when
        for(int i=0;i<n;i++){
            arr[i]=Integer.parseInt(token.nextToken()); // 입력
        }
        seq[0]=1;
        for(int i=1;i<n;i++){
            seq[i]=1;   // 1로 초기화
            for(int j=0;j<i;j++){

                if(arr[j]<arr[i]&&seq[i]<=seq[j]){ // ex) 1번째보다 2번째가 더크고
                    seq[i]=seq[j]+1;     // 수열 2번째보다 1번째가 더크거나같을때
                }
            }
        }
        // then
        int max=0;
        for(int i : seq){
            max=Math.max(max,i);
        }
        System.out.println(max);
        br.close();
    }
}


```



