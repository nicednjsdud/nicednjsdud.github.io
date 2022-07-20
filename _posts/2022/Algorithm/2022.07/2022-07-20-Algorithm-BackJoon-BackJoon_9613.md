---
published: true
title: BackJoon Algorithm 9613 GCD 합 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: GCD 합
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9613.png)

## 풀이

- 수가 백자리 수까지 입력이 가능하므로 int sum 보다는 long sum을 써준다
- 배열을 만들어 모든 경우의수에 최대공약수를 얻을수 있게한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_9613 {
    public static int GCD(int num1, int num2) {
        if (num2 == 0) {
            return num1;
        } else {
            return GCD(num2, num1 % num2);
        }
    }

    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token;
        StringBuilder sb = new StringBuilder();
        int test_count = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < test_count; i++) {
            token = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(token.nextToken());
            long sum = 0;                   // GCD의 합
            int arr[] = new int[n];         // 입력 받을 수 배열 생성
            for (int j = 0; j < n; j++) {
                arr[j] = Integer.parseInt(token.nextToken());
            }
            for (int j = 0; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    sum += GCD(arr[j], arr[k]);
                }
            }
            sb.append(sum+"\n");

        }
        // then
        br.close();
        System.out.println(sb);
    }
}



```
