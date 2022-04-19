---
title: BackJoon Algorithm 2309 일곱 난쟁이
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 일곱 난쟁이
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-08 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2309.png)




## 풀이

* 합이 100이므로 총9명 - 100을 하면 나머지 스파이2명에 합이 나온다.
* 2중 for문을 돌려서 합이 맞는 두 스파이를 잡아낸다.


```java

import java.util.Arrays;
import java.util.Scanner;

public class Back_2309 {
    public static void main(String[] args){
        //1.입 력
        Scanner sc = new Scanner(System.in);
        //1.1 난쟁이들 수입력
        int nan[]=new int[9];
        //1.2 합 ,합오차 입력
        int sum=0;
        int remainder=100;
        int spyA=0;
        int spyB=0;
        //1.3 난쟁이들 9명 수 입력받기
        for(int i=0;i<nan.length;i++){
            nan[i]=sc.nextInt();
        }
        //2.1 난쟁이들 총합 계산(9명)
        for(int i=0;i< nan.length;i++){
            sum+=nan[i];
        }
        //2.2 나머지 계산 (sum-100)
        remainder=sum-remainder;
        //2.3 나머지랑 맞는 두사람 제거
        for(int i=0;i<nan.length;i++){
            for(int j=1;j< nan.length;j++){
                if(nan[i]+nan[j]==remainder){
                    spyA=nan[i];
                    spyB=nan[j];

                }
            }
        }
        //2.4 오름차순 정렬
        Arrays.sort(nan);
        //3.1 출력
        for(int i=0;i<nan.length;i++){
            if(nan[i]==spyA || nan[i]==spyB){
                continue;
            }
            System.out.println(nan[i]);
        }

    }
}

```


