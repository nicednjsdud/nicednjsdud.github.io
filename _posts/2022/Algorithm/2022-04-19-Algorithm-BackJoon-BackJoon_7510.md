---
title: BackJoon Algorithm 7510 고급수학
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 고급수학
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

![alt](/assets/images/post/Algorithm/7510.png)



## 풀이

* 배열로 받아 오름차순 정렬함수인 Arrays를 이용
* 피타고라스 공식


```java
    import java.util.Arrays;
import java.util.Scanner;

public class Back_7510 {
    public static void main(String[] args) {

        // 1. given
        Scanner sc = new Scanner(System.in);
        int test_count=sc.nextInt();
        int arr[]=new int [3];          // 삼각형
        for(int i=0;i<test_count;i++){
            for(int j=0;j<3;j++){       // 변 3개입력
              arr[j]=sc.nextInt();
            }
            Arrays.sort(arr);           // 오름차순 정렬로 빗변 찾기
            
            // 직각 삼각형 검사
            if((arr[2]*arr[2])==(arr[1]*arr[1])+(arr[0]*arr[0])){ 
                System.out.println("Scenario #"+(i+1)+":");
                System.out.println("yes");
            }
            else{
                System.out.println("Scenario #"+(i+1)+":");
                System.out.println("no");
            }
            System.out.println();
        }
        sc.close();
    }
}
```


