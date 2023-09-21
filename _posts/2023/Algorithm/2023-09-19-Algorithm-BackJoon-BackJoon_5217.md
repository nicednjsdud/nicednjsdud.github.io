---
published: true
title: BackJoon Algorithm 쌍의합 5217 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-09-19 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5217.png)

## 풀이

```java
// 처음 풀었던 5217 알고리즘 문제

//import java.io.BufferedReader;
//import java.io.IOException;
//import java.io.InputStreamReader;
//
//public class Back_5217 {
//    public static void main(String[] args) throws IOException {
//
//        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
//        StringBuilder sb = new StringBuilder();
//        int T = Integer.parseInt(br.readLine());
//
//        for (int i = 0; i < T; i++) {
//            int num = Integer.parseInt(br.readLine());
//            int temp = num / 2;
//            sb.append("Pairs for ").append(num).append(":");
//            for (int j = 1; j <= temp; j++) {
//                if (j + j != num) {
//                    sb.append(" " + j + " " + (num - j)).append(",");
//                }
//            }
//            String str = sb.substring(0, sb.length() - 1);
//            sb = new StringBuilder();
//            sb.append(str).append("\n");
//        }
//        System.out.println(sb);
//        br.close();
//    }
//}

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_5217 {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for(int i = 0; i < T; i++) {
            int n = Integer.parseInt(br.readLine());
            //출력 값을 저장할 문자열.
            String S = "Pairs for " + n + ": ";

            for(int j = 1; j <= n / 2; j++) {

                //쌍이 서로 같지 않을때만 문자열 추가
                if(j != (n - j)) {

                    if(j > 1) {
                        S += ", ";
                    }
                    S += j + " " + (n - j);
                }
            }
            //출력
            System.out.println(S);
        }
    }

}


```
