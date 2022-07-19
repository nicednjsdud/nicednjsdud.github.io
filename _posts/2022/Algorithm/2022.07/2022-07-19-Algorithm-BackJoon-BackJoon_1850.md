---
published: true
title: BackJoon Algorithm 1850 최대공약수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 최대공약수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-19 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1850.png)

## 풀이

- 뭔가 처음봤을때는 이게뭐지..? 했는데 생각해보니 문제2를 보면 최대공약수가 3인데  
  답은 111이다
- 최대공약수 수 만큼 1을 출력하는 되는 문제였다.

```java
import java.io.*;
import java.util.StringTokenizer;

public class Back_1850 {

    public static long GCD(long num1, long num2) {
        while (num2 > 0) {
            long temp = num1;
            num1 = num2;
            num2 = temp % num2;
        }
        return num1;
    }

    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token=new StringTokenizer(br.readLine());
        long num1 = Long.parseLong(token.nextToken());
        long num2 = Long.parseLong(token.nextToken());
        // when
        long gcd = GCD(Math.max(num1,num2),Math.min(num1,num2));
        for(int i=0;i<gcd;i++){
            sb.append("1");
        }
        // then
        bw.write(sb.toString());
        bw.flush();
        br.close();
        bw.close();
    }
}


```
