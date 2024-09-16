---
published: true
title: BackJoon Algorithm List of Unique Numbers 13144 (Java)
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
last_modified_at: "2024-09-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/13144.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_13144 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // 수열의 길이 N을 입력 받음
        int N = Integer.parseInt(br.readLine());

        // 수열을 저장할 배열 생성
        int arr[] = new int[N];

        // 방문 여부 체크 배열 생성 (100001로 선언, 문제에서 숫자가 1 ~ 100000 범위로 주어짐)
        boolean isVisited[] = new boolean[100001];

        // 수열 입력 받기
        StringTokenizer token = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(token.nextToken());
        }

        // 부분 수열 개수를 카운트할 변수
        long count = 0;  // long으로 변경하여 큰 값도 처리 가능하도록 함

        // 두 포인터를 이용한 투포인터 알고리즘
        for (int st = 0, en = 0; st < N; st++) {
            // en을 증가시키며 중복되지 않는 최대 범위를 찾음
            while (en < N && !isVisited[arr[en]]) {
                isVisited[arr[en]] = true;
                en++;
            }

            // st를 시작으로 en까지의 서로 다른 숫자로 이루어진 부분 수열 개수를 더함
            count += (en - st);

            // st가 다음 위치로 넘어갈 때, 방문 체크 해제
            isVisited[arr[st]] = false;
        }

        // 결과 출력
        System.out.println(count);
        br.close();
    }
}

```
