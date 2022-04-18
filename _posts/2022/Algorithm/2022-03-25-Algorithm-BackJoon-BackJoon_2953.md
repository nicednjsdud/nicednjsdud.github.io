---
title: BackJoon Algorithm 2953 나는 요리사다
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나는 요리사다
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2953.png)



## 풀이

* 2차 배열 활용

```java
import java.util.Scanner;

public class Back_2953 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 입력
        int num=0;
        int max=0;
        // 배열로 담기
        int arr[][]=new int[5][4];
        for(int i=0;i<5;i++){
            int sum=0;
            for(int j=0;j<4;j++){
                arr[i][j]=sc.nextInt();
                sum+=arr[i][j];
            }
            if(max<sum){
                max=sum;
                num=i+1;
            }
        }
        System.out.println(num+" "+max);
        sc.close();


    }
}


```

