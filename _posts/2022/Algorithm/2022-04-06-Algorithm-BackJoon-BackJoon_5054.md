---
title: BackJoon Algorithm 5054 주차의신
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 주차의신
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-06 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5054.png)


## 풀이

* 오름 차순 정렬

```java
import java.util.Arrays;
import java.util.Scanner;

public class Back_5054 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int test_count=sc.nextInt();            // 테스트 개수 입력
        while(test_count!=0){
            int store_count=sc.nextInt();       // 상점 개수 입력
            int sum =0;
            int arr[]=new int[store_count];     // 상점 개수 거리입력
            for(int i=0;i<store_count;i++){
                arr[i]=sc.nextInt();
            }
            Arrays.sort(arr);                   // 오른 차순 정렬

            sum=(arr[arr.length-1]-arr[0])*2;
            System.out.println(sum);
            test_count--;

        }
        sc.close();
    }
}

```

