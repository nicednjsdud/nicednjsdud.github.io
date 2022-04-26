---
title: BackJoon Algorithm 1834 나머지와 몫이 같은 수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나머지와 몫이 같은 수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-07 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1834.png)




## 풀이

* 나머지는 자연수 N을 넘을수 없음.
* 몫 이랑 나머지랑 같을려면 N이하여야함


```java
import java.util.Scanner;

public class Back_1834 {
    public static void main(String[] args){
        //1.입력
        Scanner sc=new Scanner(System.in);
        // 1-1. 자연수 N 입력
        long N = sc.nextInt();             
        long sum=0;                            //몫 이랑 나머지랑 같을려면 N이하여야함
        long num1=0;
        sc.close();
        for(int i=1;i<N;i++){
            num1=(N+1)*i;
            if((num1/N)>=N){
                break;
            }
            if(N==1){
                System.out.println(1);
            }
            sum+=num1;
        }
        System.out.println(sum);
    }
}
```


