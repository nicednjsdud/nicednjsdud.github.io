---
published: true
title: BackJoon Algorithm 수들의 합 2 2003 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 수들의 합 2 2003
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2024-09-12 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2003.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2003 {
    public static void main(String[] args) throws IOException {
        // 입력을 받기 위한 BufferedReader를 사용하여 빠르게 입력 처리
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        // 첫 번째 줄 입력값 N(배열의 길이)와 M(목표 합)을 받아옴
        StringTokenizer token = new StringTokenizer(br.readLine());
        Integer N = Integer.parseInt(token.nextToken());  // 배열의 길이
        Integer M = Integer.parseInt(token.nextToken());  // 목표 합
        int arr[] = new int[N];  // N 크기의 배열 생성
        token = new StringTokenizer(br.readLine());  // 배열 요소들을 입력받음

        // 배열에 값을 입력
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(token.nextToken());
        }

        int count = 0;  // M과 같은 합을 이루는 부분 수열의 개수를 카운트
        int en;  // 배열에서의 끝 인덱스 (end)
        for (int st = 0; st < N; st++) {  // st는 배열에서 시작 인덱스 (start)
            int sum = 0;  // 현재 부분 수열의 합을 저장할 변수
            en = st;  // 끝 인덱스를 시작 인덱스와 동일하게 설정
            // sum이 M보다 작거나 같고 en이 배열을 넘지 않을 때까지 반복
            while (sum <= M && en < N) {
                sum += arr[en];  // 현재 수열의 합에 배열의 en번째 값 더하기
                if (sum == M) {  // 부분 수열의 합이 M과 같으면
                    count++;  // 부분 수열 개수 증가
                    break;  // 더 이상 같은 시작점에서 탐색을 진행하지 않음
                }
                en++;  // 끝 인덱스를 한 칸 증가시킴
            }
        }
        // M과 같은 합을 가지는 부분 수열의 개수를 출력
        System.out.println(count);
    }
}
```
