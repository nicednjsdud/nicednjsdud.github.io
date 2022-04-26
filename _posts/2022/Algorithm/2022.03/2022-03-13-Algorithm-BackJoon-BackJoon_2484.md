---
title: BackJoon Algorithm 2484 주사위 네 개
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 주사위 네 개
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-13 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2484.png)




## 풀이


```java
import java.util.Arrays;
import java.util.Scanner;

public class Back_2484 {
    public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            // 1. 입력
            int people_count = sc.nextInt();    // 사람 수
            int max=0;                          // 가장 많은 상금
          int dice_arr[]=new int[4];          // 주사위 수
            int price=0;                        // 상금

            // 2.1 주사위 수 입력
            for(int i=0;i<people_count;i++){
                dice_arr[0] = sc.nextInt();
                dice_arr[1] = sc.nextInt();
                dice_arr[2] = sc.nextInt();
                dice_arr[3] = sc.nextInt();
                // 2.2 오름차순 정렬
                Arrays.sort(dice_arr);
                if(dice_arr[2]==dice_arr[3]){
                // 2.2.1 네개의 수가 모두 같다면
                    if(dice_arr[1]==dice_arr[0] && dice_arr[2]==dice_arr[1]){
                        price = 50000+(dice_arr[3] * 5000);
                    }
                    // 2.2.2 세 개의 수만 같다면
                    else if(dice_arr[1]==dice_arr[3]||dice_arr[0]==dice_arr[3]){
                        price = 10000 + (dice_arr[3] * 1000);
                    }
                    // 2.2.3 서로 두쌍식 같은경우
                    else if (dice_arr[1]==dice_arr[0]&&dice_arr[1]!=dice_arr[3]){
                        price = 2000 + (dice_arr[3] * 500) + (dice_arr[0] * 500);
                    }
                    // 2.2.4 두개만 같은 경우
                    else{
                        price = 1000+ (dice_arr[3]*100);
                    }
                }
                else if(dice_arr[1]==dice_arr[2]){
                    // 2.3.1 세 개의 수만 같다면
                    if(dice_arr[0]==dice_arr[1]) {
                        price = 10000 + (dice_arr[2] * 1000);
                    }
                    // 2.3.2 두개만 같은 경우
                    else{
                        price = 1000 + (dice_arr[2]*100);
                    }
                }
                else if (dice_arr[0]==dice_arr[1]){
                    // 2.4.1 두개만 같은 경우
                        price = 1000+ (dice_arr[1] * 100);
                    }
                else{
                    // 2.5.1 모두 다른 경우
                    price = dice_arr[3] * 100;
                }

                // 2.6 가장 큰 상금 구하기
                if(max<price){
                    max=price;
                }


            }
            // 3. 상금 출력
            System.out.println(max);
    }    
}
```


