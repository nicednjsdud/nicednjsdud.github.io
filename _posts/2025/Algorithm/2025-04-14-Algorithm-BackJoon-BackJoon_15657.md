---
published: true
title: "🌲 백준 15657번 - DFS 트리로 이해하는 중복 조합 (N과 M 8)"
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
description: "DFS 백트래킹이 어렵다면 트리로 흐름을 시각화해보자! 백준 15657번 문제를 예제로 DFS 흐름을 트리로 따라가 봅니다."
tag: "백준, DFS, 중복조합, Java, 트리로이해하기"
article_tag1: "DFS 트리"
article_section: "알고리즘"
meta_keywords: "백준 15657, DFS 트리, 중복 조합, 백트래킹 시각화"
last_modified_at: "2025-04-25 22:05:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🌲 백준 15657번 - DFS 트리로 이해하는 중복 조합 (N과 M 8)

🔗 [문제 바로가기 - 백준 15657번](https://www.acmicpc.net/problem/15657)  
![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## 📌 문제 요약

- N개의 자연수 중에서 M개를 **중복을 허용하여** 고른 수열을 출력
- 출력은 **사전 순(오름차순)**으로 정렬되어야 함
- 즉, **중복 조합 + 정렬**

![alt](/assets/images/post/Algorithm/15657.png)

---

## ✅ 예제 입력

```
4 2
9 8 7 1
```

정렬 후: `1 7 8 9`  
즉, `input = [1, 7, 8, 9]`, `M = 2`

---

## 🧩 전체 코드 (Java)

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_15657 {

    static int N, M;
    static int[] input;
    static int[] output;

    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        input = new int[N];
        output = new int[M];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            input[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(input); // 사전순 출력을 위해 정렬
        dfs(0, 0);
        System.out.print(sb);
    }

    private static void dfs(int start, int depth) {
        if (depth == M) {
            for (int i = 0; i < M; i++) {
                sb.append(output[i]).append(" ");
            }
            sb.append('\n');
            return;
        }

        for (int i = start; i < N; i++) {
            output[depth] = input[i];
            dfs(i, depth + 1); // 중복 허용
        }
    }
}
```

---

## 🌲 DFS 트리 흐름 구조 (depth = 0 → M까지)

```
depth = 0
├── 1 → dfs(0, 1)
│   ├── 1 → dfs(0, 2) → 출력: 1 1
│   ├── 7 → dfs(1, 2) → 출력: 1 7
│   ├── 8 → dfs(2, 2) → 출력: 1 8
│   ├── 9 → dfs(3, 2) → 출력: 1 9
├── 7 → dfs(1, 1)
│   ├── 7 → dfs(1, 2) → 출력: 7 7
│   ├── 8 → dfs(2, 2) → 출력: 7 8
│   ├── 9 → dfs(3, 2) → 출력: 7 9
├── 8 → dfs(2, 1)
│   ├── 8 → dfs(2, 2) → 출력: 8 8
│   ├── 9 → dfs(3, 2) → 출력: 8 9
├── 9 → dfs(3, 1)
    ├── 9 → dfs(3, 2) → 출력: 9 9
```

---

## ✅ 출력 결과

```
1 1
1 7
1 8
1 9
7 7
7 8
7 9
8 8
8 9
9 9
```

---

## 🔍 흐름 설명

- **`dfs(start, depth)`**
  - `start`는 오름차순 유지를 위해 사용
  - `depth`는 현재까지 선택한 숫자의 개수
- **`dfs(i, depth + 1)`**
  - 중복 허용이므로 현재 i부터 다시 시작 가능

---

## 💡 핵심 요약

| 요소          | 설명                    |
| ------------- | ----------------------- |
| 중복 허용     | ✅ `dfs(i, ...)` 호출   |
| 오름차순 유지 | ✅ `i = start`부터 탐색 |
| visited 배열  | ❌ 필요 없음            |
| 출력 시점     | `depth == M`일 때       |

---
