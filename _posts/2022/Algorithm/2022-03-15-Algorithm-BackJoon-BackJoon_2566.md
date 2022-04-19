---
title: BackJoon Algorithm 2566 최댓값
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 최댓값
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-15 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2566_1.png)
![alt](/assets/images/post/Algorithm/2566_2.png)



## 풀이

* 2차 배열을 활용하여 행과 열을 구하다.

```java
import java.util.Scanner;

public class Back_2566 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
      //     given
        int max=0;
        int arr[][]=new int[9][9];
        int row=0;
        int col=0;
        //    when
        for(int i=0;i<9;i++){
            for(int j=0;j<9;j++){
                arr[i][j] = sc.nextInt();
                if(max<arr[i][j]){
                    max=arr[i][j];
                    row=i+1;
                    col=j+1;
                }
            }
        }
        //    then
        System.out.println(max);
        System.out.println(row+" "+col);
        sc.close();


    }
}

```


