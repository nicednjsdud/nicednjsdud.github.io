---
published: true
title: BackJoon Algorithm 연속합 1912 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 누울 자리를 찾아라
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-01-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1912_1.png)
![alt](/assets/images/post/Algorithm/1912_2.png)

## 풀이

- 맞은 풀이는 밑에 있습니다.
- (시간 초과 나온 풀이)
- 재귀함수를 쓰지않고 루프를 돌려서 풀어봤다.
- 하지만 시간초과가 나왔다..

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1912 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int arr[] = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        int sum = arr[0];
        for (int i = 0; i < n; i++) {   // 10개 돌리고
            int size = i+1;
            while(size <= n){
                int temp_sum = 0;
                for (int j = i; j < size; j++) {   // 앞에서 하나씩 빼면서 돌리고
                    temp_sum += arr[j];
                }
                if(temp_sum > sum){
                    sum = temp_sum;
                }
                size ++ ;
            }
        }
        System.out.println(sum);
    }
}

```

- (맞은 풀이)
- 재귀함수를 사용해서 그전에 합 (i + (i+1))에 (i+2)를 더하면 되는 문제였다.
- 재귀함수를 더 공부해야겠다.

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1912 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int arr[] = new int[n];
        int dp[] = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        dp[0] = arr[0];
        int sum = arr[0];
        for (int i = 1; i < n; i++) {
            dp[i] = Math.max(dp[i - 1] + arr[i], arr[i]);       // 재귀

            sum = Math.max(sum, dp[i]);
        }
        System.out.println(sum);
    }
}
```
