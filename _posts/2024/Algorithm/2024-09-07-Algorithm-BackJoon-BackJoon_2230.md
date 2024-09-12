---
published: true
title: BackJoon Algorithm 수고르기 2230 .(Java)
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
last_modified_at: "2024-09-07 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2230.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_2230 {
    public static void main(String[] args) throws IOException {
        // 입력을 받기 위한 BufferedReader 사용
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // 첫 줄에 입력된 N(수열의 길이), M(최소 차이)을 받음
        StringTokenizer token = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(token.nextToken()); // 수열의 길이 N
        int M = Integer.parseInt(token.nextToken()); // 최소 차이 M

        // N개의 수를 담을 배열 선언
        int[] arr = new int[N];

        // 배열에 수열 값 입력 받기
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine()); // 각 숫자를 배열에 저장
        }

        // 결과값을 저장할 변수 'min'을 초기화, Integer.MAX_VALUE로 시작
        int min = Integer.MAX_VALUE; // 최소 차이를 찾기 위한 변수

        // 투 포인터 중 뒤쪽 포인터(en)를 0으로 초기화
        int en = 0;

        // 수열을 오름차순으로 정렬 (투포인터는 정렬된 배열에서 효과적)
        Arrays.sort(arr);

        // 첫 번째 포인터(st)를 0부터 시작해서 N까지 이동
        for(int st = 0; st < N; st++) {
            // 두 번째 포인터(en)가 수열의 끝을 넘지 않고, arr[en] - arr[st]가 M보다 작은 동안 en을 증가
            while(en < N && arr[en] - arr[st] < M) {
                en++; // 조건을 만족하지 않으면 en을 앞으로 이동
            }
            // en이 범위를 넘어가면 더 이상 검사할 필요 없음
            if(en == N) break;

            // 조건을 만족하는 차이를 찾으면 그 차이를 min과 비교해 최소값을 저장
            min = Math.min(min, arr[en] - arr[st]); // arr[en] - arr[st] >= M인 최소값 찾기
        }

        // 최소 차이값 출력
        System.out.println(min);
    }
}



```
