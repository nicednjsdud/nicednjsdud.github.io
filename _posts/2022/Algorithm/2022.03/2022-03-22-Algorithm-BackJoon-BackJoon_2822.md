---
title: BackJoon Algorithm 2822 점수 계산
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 점수 계산
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-22 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2822.png)



## 풀이

* 순서를 셀 배열과 오름차순 정렬을 할배열을 생성한다.
* 5칸 배열에 오름차순 정렬한 큰 점수 5개를 복사한다.


```java
import java.util.Arrays;
import java.util.Scanner;

public class Back_2822 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int arr[]=new int[8];
        int arr2[]=new int[5];
        int arr3[]=new int[8];
        for(int i=0;i<arr.length;i++){
            arr[i]=sc.nextInt();
            arr3[i]=arr[i];
        }
        Arrays.sort(arr);
        int sum=0;
        for(int i=3;i<arr.length;i++){
            arr2[i-3]=arr[i];
            sum+=arr2[i-3];
        }
        System.out.println(sum);
        for(int i=0;i<arr3.length;i++){
            for(int j=0;j<arr2.length;j++){
                if(arr3[i]==arr2[j]){
                    System.out.print((i+1)+" ");
                }
            }
        }
        System.out.println();
        sc.close();
    }
}
```

