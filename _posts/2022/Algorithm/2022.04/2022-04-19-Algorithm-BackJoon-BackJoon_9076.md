---
title: BackJoon Algorithm 9076 점수집계
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 점수집계
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-19 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9076.png)



## 풀이

* 배열로 받아 오름차순 정렬함수인 Arrays를 이용


```java
import java.util.Arrays;
import java.util.Scanner;

public class Back_9076 {
    public static void main(String[] args) {

        // given
        Scanner sc = new Scanner(System.in);
        int test_count = sc.nextInt();      //테스트 개수
        int arr[]=new int[5];               // 점수배열
        for(int i=0;i<test_count;i++){
            for(int j=0;j<5;j++){           // 점수 입력받기
                arr[j]=sc.nextInt();
            }
        // when
            Arrays.sort(arr);               // 배열 오름차순 정렬
            if(arr[3]-arr[1]>=4){           // 4점 이상 차이나면
                System.out.println("KIN");
            }
            else if(arr[3]-arr[1]<4){
                int sum=arr[1]+arr[2]+arr[3];   // 가운의 3개의 합
                System.out.println(sum);
            }
        }
        sc.close();
    }
}
```


