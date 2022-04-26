---
title: BackJoon Algorithm 5988
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 홀수일까 짝수일까
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-13 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

    짝이 없는 경재는 매일 홀로 있다보니 홀수를 판별할 수 있는 능력이 생겼다. 
    창식이는 경재의 말이 사실인지 그 능력을 시험해보려 한다. 
    창식이의 의심이 끝이 없을 것 같아 N개만 확인하기로 정했다.

    N개의 정수가 주어지면 홀수인지 짝수인지를 출력하는 프로그램을 만들어 
    경재의 능력을 검증할 수 있게 도와주자.

## 입력

    첫 번째 줄에 숫자의 개수 N(1 <= N <= 100)이 주어진다.

    두 번째 줄부터 N+1번째 줄에 걸쳐 홀수인지 짝수인지 확인할 정수 K 
    (1 <= K <= 10^60)가 주어진다.

## 출력

    N개의 줄에 걸쳐 한 줄씩 정수 K가 홀수라면 'odd'를, 짝수라면 'even'을 출력한다.

## 풀이

* 그냥 일반적으로 풀면 런타임 에러가 나온다. 문자열 배열로 (split 함수)를 사용하여 잘라서 받는다 . 


```java
public class Back_5988 {
    public static void main(String[] args) {
        // 입력
        Scanner sc = new Scanner(System.in);
        int test_count=sc.nextInt();        // 테스트개수

       while(test_count!=0){
           String[] str=sc.next().split("");
           int num = Integer.parseInt(str[str.length-1]);
           if(num%2==0){
               System.out.println("even");
           }
           else{
               System.out.println("odd");
           }
           test_count--;
       }
    }
}
```

