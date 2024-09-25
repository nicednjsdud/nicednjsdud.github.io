---
published: true
title: BackJoon 겹치는 건 싫어 20922 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 소수의 연속합 1644
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2024-09-22 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/20922.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_20922 {
    public static void main(String[] args) throws IOException {
        // 입력을 받기 위한 BufferedReader 객체 생성
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        // 첫 번째 줄 입력: N은 배열의 길이, K는 숫자가 배열에서 나타날 수 있는 최대 빈도수
        StringTokenizer token = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(token.nextToken());  // 배열의 크기 N
        int K = Integer.parseInt(token.nextToken());  // 배열의 각 숫자가 등장할 수 있는 최대 횟수 K
        
        // 수열을 저장할 배열 선언
        int arr[] = new int[N];
        
        // 두 번째 줄 입력: N개의 숫자를 배열에 저장
        token = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(token.nextToken());
        }
        
        // 각 숫자의 등장 횟수를 저장할 배열 (숫자의 최대 범위는 1 ~ 100000)
        int[] count = new int[100001];
        
        // 최대 부분 수열의 길이를 저장할 변수와 두 포인터
        int max = 0;
        int st = 0;
        int en = 0;

        // 투 포인터 사용
        while (en < N) {
            // 현재 수의 등장 횟수가 K보다 작거나 같으면 끝 포인터를 확장
            if (count[arr[en]] < K) {
                count[arr[en]]++;  // 숫자 카운트 증가
                en++;  // 끝 포인터 확장
                max = Math.max(max, en - st);  // 최대 길이 업데이트
            } else {
                // 만약 arr[en]이 이미 K번 등장했다면, 시작 포인터를 오른쪽으로 이동시킴
                count[arr[st]]--;  // 시작 포인터가 가리키는 숫자의 카운트를 감소
                st++;  // 시작 포인터를 오른쪽으로 이동
            }
        }
        
        // 결과 출력: 조건을 만족하는 부분 수열의 최대 길이
        System.out.println(max);
    }
}



```
