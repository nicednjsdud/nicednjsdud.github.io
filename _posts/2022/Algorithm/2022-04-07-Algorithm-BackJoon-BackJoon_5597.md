---
title: BackJoon Algorithm 5597
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 과제 안 내신 분..?
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-07 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5597_1.png)
![alt](/assets/images/post/Algorithm/5597_2.png)
![alt](/assets/images/post/Algorithm/5597_3.png)

## 풀이

* 한사람의 번호를 기본값0인 배열에 집어넣는다.
* 기본값(0)인사람의 번호를 출력 (배열은 0부터 시작하니 총 31공간의 배열 생성)

```java
iimport java.util.Scanner;

public class Back_5597 {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //1. 입력
        int arr[]=new int[31];
        for(int i=1;i<29;i++){
            int clear=sc.nextInt();   // 과제 한사람 번호입력
            arr[clear]=1;             // 과제 한번호는 1로 변경
        }
        for(int i=1;i<arr.length;i++){
            if(arr[i]!=1){
                System.out.println(i);  // 과제안한사람 ( 0 ) 출력
            }
        }
        sc.close();
    }
}

```

