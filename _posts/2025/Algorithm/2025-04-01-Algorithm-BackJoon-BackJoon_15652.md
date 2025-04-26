---
published: true
title: "🔢 백준 15652번 - N과 M (4) (DFS/백트래킹)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 15652번 N과 M (4) 문제의 Java 풀이. 중복 조합을 DFS로 해결하는 방법과 핵심 포인트를 정리"
tag: "백준, Java, DFS, 중복 조합"
article_tag1: "백트래킹"
article_section: "알고리즘"
meta_keywords: "백준, Java, DFS, 백트래킹, 중복 조합, 알고리즘"
last_modified_at: "2025-04-01 18:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🔢 백준 15652번 - N과 M (4)

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## 🧩 문제 설명

- 자연수 N과 M이 주어졌을 때,
- 1부터 N까지 자연수 중 **M개를 뽑되**, **같은 수를 여러 번 골라도 되고**
- **비내림차순(오름차순 포함)**인 수열을 모두 구하는 문제입니다.

![alt](/assets/images/post/Algorithm/15652_1.png)
![alt](/assets/images/post/Algorithm/15652_2.png)

---

## 💡 문제 조건 요약

| 조건      | 내용                                                 |
| --------- | ---------------------------------------------------- |
| 숫자 범위 | 1 ~ N                                                |
| 뽑는 개수 | M개                                                  |
| 중복 허용 | ✅ 가능                                              |
| 순서 중요 | ❌ 비내림차순만 허용                                 |
| 정렬      | 오름차순 또는 같은 숫자 허용 (ex. 1 1 2, 2 2 2 가능) |

---

## 📥 입력 예시

```
3 2
```

---

## 📤 출력 예시

```
1 1
1 2
1 3
2 2
2 3
3 3
```

---

## 🧠 핵심 아이디어

이 문제는 **"중복 조합 (Combination with Repetition)"** 문제입니다.

- 중복은 허용되지만 **순서만 정렬된 형태**여야 하기 때문에 `start` 값을 재귀로 넘겨주며 오름차순을 유지합니다.
- 즉, 이전에 선택한 숫자 이상부터만 다시 고를 수 있도록 합니다.

---

## ✅ Java 코드 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_15652 {
    public static int[] arr;
    public static int N, M;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        arr = new int[M];

        dfs(1, 0); // 1부터 시작, 깊이는 0
    }

    private static void dfs(int start, int depth) {

        if (depth == M) {
            for (int i : arr)
                System.out.print(i + " ");
            System.out.println();
            return;
        }

        for (int i = start; i <= N; i++) {
            arr[depth] = i;        // 현재 위치에 숫자 저장
            dfs(i, depth + 1);     // 중복 허용 → i부터 다시 탐색
        }
    }
}
```

---

## 🔍 코드 해설

### 1️⃣ `dfs(start, depth)` 함수

| 매개변수 | 의미                                                  |
| -------- | ----------------------------------------------------- |
| `start`  | 현재 선택 가능한 최소 숫자 (중복 허용, 오름차순 유지) |
| `depth`  | 현재까지 선택한 수의 개수 (M에 도달하면 출력)         |

---

### 2️⃣ 기저 조건

```java
if (depth == M) {
    for (int i : arr) System.out.print(i + " ");
    System.out.println();
    return;
}
```

- M개의 수를 모두 골랐으면 현재 조합을 출력하고 return.

---

### 3️⃣ 중복 조합 로직

```java
for (int i = start; i <= N; i++) {
    arr[depth] = i;
    dfs(i, depth + 1); // 중복 허용 → i부터 시작
}
```

- 중복 허용이기 때문에 `dfs(i, depth + 1)`로 호출
- 일반 순열이라면 `dfs(i + 1, ...)`로 했겠지만, 여기서는 같은 숫자도 다시 사용할 수 있음

---

## 📌 시간 복잡도

- 최악의 경우 `O(N^M)` 정도
- `N=7`, `M=7` 정도까지는 충분히 탐색 가능

---

## ✅ 정리

| 항목          | 설명                                |
| ------------- | ----------------------------------- |
| 문제 유형     | 백트래킹 + 중복 조합                |
| 중복 허용     | O                                   |
| 오름차순 유지 | O (`start` 이용)                    |
| DFS 탐색 방식 | 현재 숫자부터 다시 탐색 (중복 허용) |

---
