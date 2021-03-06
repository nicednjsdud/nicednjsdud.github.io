---
published: true
title: BackJoon Algorithm 1934 최소공배수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 최소공배수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1934.png)

## 풀이

- 먼저 최대공약수를 구하고 최소공배수로 구해주는 방식을 선택했다.
- 최대공약수는 재귀함수를 통해서 풀어야 한다.
- 최소공배수는 두수를 곱한뒤 최대공약수로 나눠주면된다!

```java
import java.io.*;
import java.util.StringTokenizer;

public class Back_1934 {

    // 최대 공약수 구하기
    public static int GCD(int num1,int num2){
        if(num2==0){
            return num1;
        }
        else{
            return GCD(num2,num1%num2);
        }
    }
    // 최소 공배수 구하기
    public static int LCM(int num1,int num2){
        return num1 * num2 / GCD(num1,num2);
    }
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer token;
        int test_count = Integer.parseInt(br.readLine());
        // when
        for(int i=0;i<test_count;i++){
            token=new StringTokenizer(br.readLine());
            int num1 = Integer.parseInt(token.nextToken());
            int num2 = Integer.parseInt(token.nextToken());
            int gcd_result= GCD(num1,num2);
            int lcm_result= LCM(num1,num2);
            bw.write(lcm_result+"\n");
        }
        // then
        bw.flush();
        bw.close();
        br.close();
    }
}


```
