---
title: BackJoon Algorithm 2798 블랙잭
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 블랙잭
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

![alt](/assets/images/post/Algorithm/2798.png)



## 풀이

* 삼중 for문을 활용하여 배열에 연속으로 나오는3개를 합한다.


```java
import java.util.Scanner;

public class Back_2798 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        int card_count=sc.nextInt();
        int max=sc.nextInt();
        int arr[] = new int[card_count];
        int tmp=0;
        int sum=0;
        //when
        for(int i=0;i<card_count;i++){
                arr[i]=sc.nextInt();
        }
        for(int i=0;i<card_count;i++){
            for(int j=i+1;j<card_count;j++){
                for(int k=j+1;k<card_count;k++){
                        sum=(arr[i]+arr[j]+arr[k]);
                        if(tmp<sum&&sum<=max){
                            tmp=sum;
                        }

                    }

                }
            }
        //then
        System.out.println(tmp);
        sc.close();
        }
    }
```

