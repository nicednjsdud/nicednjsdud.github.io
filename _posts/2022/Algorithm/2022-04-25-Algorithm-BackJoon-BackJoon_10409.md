---
title: BackJoon Algorithm 10409 서버
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
last_modified_at: '2022-04-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10409.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* 입력시간을 배열로 받아 T시간 이상이면 반복문을 break;한다.

```java



import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10409 {
    public static void main(String[] args) throws Exception{
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer token = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(token.nextToken());    // 테스트 개수 입력 받기
        int T = Integer.parseInt(token.nextToken());    // 시간 입력받기
        int arr[] =new int[n];                          // n개의 입력시간 받기
        int sum=0;
        int count=0;
        //when
        token = new StringTokenizer(br.readLine());
        for(int i=0;i<n;i++) {
            arr[i] = Integer.parseInt(token.nextToken());
        }
        //then
        for(int i=0;i<n;i++){
            sum+=arr[i];
            if(sum>T){
                break;
            }
            count++;

        }
        System.out.println(count);
        br.close();
    }
}
```


