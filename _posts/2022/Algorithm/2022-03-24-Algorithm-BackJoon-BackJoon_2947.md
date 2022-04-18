---
title: BackJoon Algorithm 2947 나무조각
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나무조각
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-24 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2947.png)



## 풀이

* 2차 배열 활용

```java
import java.util.Scanner;

public class Back_2947 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 나무조각 갯수
        int num =5;
        int temp=0;
        // 순서
        int arr[]=new int[5];

        // 순서 입력 받기
       for(int i=0;i<num;i++){
           arr[i]=sc.nextInt();
       }
       // 순서 오름차순으로 바꾸기
        while(true){
            // 배열이 1,2,3,4,5 면 종료
            if(arr[0]==1&&arr[1]==2&&arr[2]==3&&arr[3]==4&&arr[4]==5){
                break;
            }
            for(int i=0;i<num-1;i++) {
                // 뒷수가 더클때 변수삽입하여 교환
                if (arr[i] > arr[i+1]) {
                    temp = arr[i+1];
                    arr[i+1] = arr[i];
                    arr[i] = temp;

                }
                // 뒷수가 작을시 건너뛰기
                else{
                 continue;
                }
                // 출력
                for(int j=0;j<num;j++){
                    System.out.print(arr[j]+" ");
                }
                System.out.println();
            }

        }

        sc.close();
        }

    }

```

