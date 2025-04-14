---
published: true
title: "🔍 백준 15655번 - N과 M (6)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - Backtracking
  - Java
description: "백준 15655번 문제를 풀며 순열과 조합을 구분하는 핵심 포인트와 잘못된 풀이를 분석합니다."
tag: "백준, Java, DFS, 조합, 백트래킹"
article_tag1: "Backtracking"
article_section: "Algorithm"
meta_keywords: "백준 15655, Java, 순열 조합 차이, DFS, 백트래킹"
last_modified_at: "2025-04-14 19:20:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🔍 백준 15655번 - N과 M (6) | 순열 vs 조합 제대로 구분하자!

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## 📌 문제 요약

> N개의 자연수 중에서 M개를 고르는 **모든 조합**을 출력하라.  
> 단, 숫자는 오름차순으로 정렬되어 주어지며,  
> **출력 역시 사전 순**이어야 한다.

![alt](/assets/images/post/Algorithm/15655.png)

---

## 🎯 입력 예시

```
4 2
9 8 7 1
```

정렬된 수열: `1 7 8 9`

---

## 🧠 문제의 핵심

- ❗ **같은 수는 한 번만 사용 가능 (중복 X)**
- ✅ 선택한 수열은 **오름차순**으로 정렬되어야 함
- ✅ 즉, **조합(Combination)** 문제입니다!

---

## ✅ 정답 풀이: `start` 인덱스를 이용한 조합 방식

```java
import java.io.*;
import java.util.*;

public class Back_15655 {

    static int N, M;
    static int[] input, output;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        input = new int[N];
        output = new int[M];

        st = new StringTokenizer(br.readLine());
        for(int i = 0; i < N; i++) {
            input[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(input); // 오름차순 정렬

        dfs(0, 0);

        System.out.print(sb);
    }

    private static void dfs(int start, int depth) {
        if (depth == M) {
            for (int i = 0; i < M; i++) {
                sb.append(output[i]).append(" ");
            }
            sb.append("\n");
            return;
        }

        for (int i = start; i < N; i++) {
            output[depth] = input[i];
            dfs(i + 1, depth + 1); // 오름차순 유지
        }
    }
}
```

---

## 🔎 코드 분석

| 부분                    | 설명                                   |
| ----------------------- | -------------------------------------- |
| `Arrays.sort(input)`    | 사전순 출력을 위한 정렬                |
| `dfs(start, depth)`     | `start`부터 탐색해서 오름차순 유지     |
| `dfs(i + 1, depth + 1)` | 다음 탐색은 현재보다 오른쪽 인덱스부터 |
| `output[]`              | 현재까지 뽑은 조합 결과 저장 배열      |
| `depth == M`            | M개를 다 뽑았을 때 출력                |

---

## 💡 순열과 조합 차이 다시 보기

| 구분      | 순열 (Permutation)    | 조합 (Combination) |
| --------- | --------------------- | ------------------ |
| 순서      | ✅ 중요               | ❌ 중요하지 않음   |
| 중복 여부 | 문제에 따라 다름      | 중복 없이 고름     |
| 로직      | visited 사용          | start index 사용   |
| 예시      | `1 2` `2 1` 모두 출력 | `1 2` 만 출력      |

---

## ✅ 출력 예시

입력:

```
4 2
9 8 7 1
```

출력:

```
1 7
1 8
1 9
7 8
7 9
8 9
```

---

## 🧠 마무리 정리

| 핵심 포인트        | 설명                                  |
| ------------------ | ------------------------------------- |
| 조합 문제          | 순서 중요 X, 오름차순 유지            |
| DFS + start 인덱스 | 중복 방지 및 정렬 유지에 적합         |
| visited 배열 ❌    | 순열에서만 사용 (이 문제엔 필요 없음) |

---
