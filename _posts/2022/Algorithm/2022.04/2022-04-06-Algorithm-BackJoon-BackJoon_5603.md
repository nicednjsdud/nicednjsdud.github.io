---
title: BackJoon Algorithm 5603
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: TGN
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-06 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5603.png)


## 풀이

* 2차 배열로 담는다.
* 광고를 하지 않았을 때 수익 < 광고를 했을 때의 수익 - 광고 비용 = 광고 O
* 광고를 하지 않았을 때 수익 > 광고를 했을 때의 수익 - 광고 비용 = 광고 x
* 광고를 하지 않았을 때 수익 = 광고를 했을 때의 수익 - 광고 비용 = 광고 상관없음

```java
import java.util.Scanner;

public class Back_5063 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int Test=sc.nextInt();                  // 테스트 케이스 입력
        int arr[][] = new int [Test][3];        // 정수 3개 입력 받을 배열 생성
        for(int i=0;i<Test;i++){
            for(int j=0;j<3;j++){
                arr[i][j]=sc.nextInt();         // 정수 3개 입력
            }
        }
        for(int i=0;i<Test;i++){
                if(arr[i][0]<(arr[i][1]-arr[i][2])){
                    System.out.println("advertise");
                }
                else if(arr[i][0]>(arr[i][1]-arr[i][2])){
                    System.out.println("do not advertise");
                }
                else if(arr[i][0]==(arr[i][1]-arr[i][2])){
                    System.out.println("does not matter");
                }

        }

        sc.close();

    }
}

```

