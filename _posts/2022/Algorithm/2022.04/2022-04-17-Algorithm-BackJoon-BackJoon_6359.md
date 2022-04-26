---
title: BackJoon Algorithm 6359
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 만취한 상범
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-17 14:12:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm_6359
========================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

    서강대학교 곤자가 기숙사의 지하에는 n개의 방이 일렬로 늘어선 감옥이 있다. 
    각 방에는 벌점을 많이 받은 학생이 구금되어있다.

    그러던 어느 날, 감옥 간수인 상범이는 지루한 나머지 정신나간 게임을 하기로 결정했다.
    게임의 첫 번째 라운드에서 상범이는 위스키를 한 잔 들이키고, 달려가며 감옥을 한 개씩
    모두 연다. 그 다음 라운드에서는 2, 4, 6, ... 번 방을 다시 잠그고, 세 번째
    라운드에서는 3, 6, 9, ... 번 방이 열려있으면 잠그고, 잠겨있다면 연다. k번째
    라운드에서는 번호가 k의 배수인 방이 열려 있으면 잠그고, 잠겨 있다면 연다. 이렇게 
    n번째 라운드까지 진행한 이후, 상범이는 위스키의 마지막 병을 마시고 쓰러져 잠든다.

    구금되어있는 몇 명(어쩌면 0명)의 학생들은 자신의 방을 잠그지 않은 채 상범이가 
    쓰러져버렸단 것을 깨닫고 즉시 도망친다.

    방의 개수가 주어졌을 때, 몇 명의 학생들이 도주할 수 있는지 알아보자.

## 입력

    입력의 첫 번째 줄에는 테스트 케이스의 개수 T가 주어진다. 
    각 테스트 케이스는 한 줄에 한 개씩 방의 개수 n(5 ≤ n ≤ 100)이 주어진다.

## 출력

    한 줄에 한 개씩 각 테스트 케이스의 답, 즉 몇 명이 탈출할 수 있는지를 출력한다.

## 풀이

* 배열로 받아서 카운트를 ++하여 체크한다.

```java
import java.util.Scanner;

public class Back_6359 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int test_count= sc.nextInt();   // 테스트 갯수
        // 배열은 0부터 시작하니 0을 제외 하고 구한다.
        for(int i=0;i<test_count;i++){
            int room_count=sc.nextInt();  // 방 개수
            int arr[]=new int[room_count+1];    // 방
            if(room_count==0){
                System.out.println(room_count);
                break;
            }
            int count=1;    // open close 체크카운트
            for(int j=1;j<arr.length;j++){      // 1이 open 0이 close
                for(int k=1;k<arr.length;k++){
                    if(k%count==0){
                        if(arr[k]==1){
                            arr[k]=0;
                        }
                        else if(arr[k]==0){
                            arr[k]=1;
                        }
                    }
                    else{
                        continue;
                    }
                }
                count++;
            }
            int open_count=0;
            for(int w=1;w<arr.length;w++){

                if(arr[w]==1) {
                    open_count++;
                }
            }
            System.out.println(open_count);
        }

        sc.close();
    }
}
```

