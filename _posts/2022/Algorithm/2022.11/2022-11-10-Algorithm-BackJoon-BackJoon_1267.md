---
published: true
title: BackJoon Algorithm 핸드폰 요금 1267 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 핸드폰 요금
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-10 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1267.png)

## 풀이

- 만약 30초부터 59초, 만약 60초부터 119초 사이 이 두문장을 조심해서 하면 된다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1267 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int Y_price = 0;
        int M_price = 0;
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            int call_time = Integer.parseInt(st.nextToken());
            // when
            // 입력한 수에서 영식 / 만식을 각 통화의 개수에 대입
            // 전화시간이 60초 아래면
            if (call_time < 60) {
                if (call_time < 30) {
                    Y_price += 10;
                } else {
                    Y_price += 20;
                }
                M_price += 15;
            } else {
                Y_price += (call_time / 30 + 1) * 10;
                M_price += (call_time / 60 + 1) * 15;
            }
        }
        // then
        if (Y_price > M_price) {
            System.out.println("M " + M_price);
        } else if (Y_price < M_price) {
            System.out.println("Y " + Y_price);
        } else {
            System.out.println("Y M " + Y_price);
        }
        br.close();
    }
}



```
