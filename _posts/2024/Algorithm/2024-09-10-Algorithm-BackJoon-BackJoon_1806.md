---
published: true
title: BackJoon Algorithm 부분합 1806 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 부분합 1806
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2024-09-10 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1806.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1806 {
    public static void main(String[] args) throws IOException {
        // BufferedReader를 사용해 입력을 읽음
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // 첫 번째 줄에서 N(배열 크기)와 M(목표합)을 읽어옴
        StringTokenizer token = new StringTokenizer(br.readLine());

        // N: 배열의 크기, M: 부분합이 넘겨야 하는 기준
        int N = Integer.parseInt(token.nextToken());
        int M = Integer.parseInt(token.nextToken());

        // 두 번째 줄에서 배열 값을 읽어옴
        token = new StringTokenizer(br.readLine());
        int arr[] = new int[N];
        // 배열에 N개의 값을 저장
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(token.nextToken());
        }

        // 초기 값 설정: 부분합(total)은 첫 번째 원소로 시작
        int total = arr[0];
        // 'en'은 끝 포인터, 'st'는 시작 포인터
        int en = 0;
        // 최소 길이를 저장할 변수, 처음에는 큰 값으로 설정
        int min = Integer.MAX_VALUE;

        // 투 포인터 알고리즘 시작, 시작 포인터 'st'를 기준으로 반복
        for (int st = 0; st < N; st++) {
            // 부분합이 M보다 작고 끝 포인터가 배열 범위 내에 있을 때까지 'en'을 증가시킴
            while (en < N && total < M) {
                en++;
                // 'en'이 범위 내에 있으면 배열 값을 더함
                if (en != N) total += arr[en];
            }
            // 만약 'en'이 배열 범위를 넘어가면 종료
            if (en == N) break;
            // 최소 길이를 계산하여 갱신
            min = Math.min(min, en - st + 1);
            // 시작 포인터 값을 부분합에서 빼고 다음 'st'로 넘어감
            total -= arr[st];
        }

        // 만약 부분합을 만족하는 구간이 없으면 min을 0으로 설정
        if (min == Integer.MAX_VALUE) min = 0;
        // 결과 출력
        System.out.println(min);
    }

}

```
