---
published: true
title: "🔍 백준 15654번 - N과 M (5)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - DFS
  - Java
description: "백준 15654번 - N과 M (5) 문제를 DFS로 하나하나 직접 따라가며 완벽히 이해하는 순열 생성 과정 정리"
tag: "백준, DFS, 순열, 백트래킹, Java"
article_tag1: "DFS"
article_section: "알고리즘"
meta_keywords: "백준 15654, DFS, 순열, 백트래킹, Java 알고리즘"
last_modified_at: "2025-02-21 18:20:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🔍 백준 15654번 - N과 M (5) | DFS 순열 로직 완전 정복

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## 📌 문제 요약

- 자연수 N개가 주어지고, 그 중 M개를 **중복 없이 골라 순열**을 만들어야 함
- 출력은 **사전 순으로 오름차순**
- 예: `1 2`, `2 1`, `1 3`, `3 1`, `2 3`, ...

![alt](/assets/images/post/Algorithm/15654.png)

---

## 📥 예제 입력

```
3 2
3 1 2
```

정렬되면: `[1, 2, 3]`  
→ 이 숫자들로 M = 2인 순열을 만들어야 함 (중복 ❌)

---

## ✅ 핵심 포인트

| 포인트     | 설명                                |
| ---------- | ----------------------------------- |
| 중복 허용? | ❌ 안됨                             |
| 정렬 필요? | ✅ 사전순 출력을 위해 오름차순 정렬 |
| 자료구조   | `visited[]` 배열로 중복 체크        |
| 백트래킹   | 사용한 숫자 되돌리기                |

---

## 🧠 DFS 구조 이해하기

```java
dfs(depth)
```

- `depth == M` → 출력
- `for i in 0 ~ N-1`
  - `visited[i] == false` → 사용 가능
  - 숫자 저장 후 `dfs(depth + 1)`
  - 백트래킹: `visited[i] = false` 복원

---

## 📚 시뮬레이션으로 완전 이해하기

### 🎯 초기 상태

```java
N = 3, M = 2
입력: 3 1 2 → 정렬: [1, 2, 3]
```

```java
dfs(0) 시작
```

---

### ✅ dfs(0)

- depth = 0
- visited = `[false, false, false]`
- output = `[]`

```text
i = 0 → 1 사용
→ visited[0] = true
→ output[0] = 1
→ dfs(1) 호출
```

---

### ✅ dfs(1)

- depth = 1
- output = `[1, _]`
- visited = `[true, false, false]`

```text
i = 1 → 2 사용
→ output = [1, 2]
→ visited = [true, true, false]
→ dfs(2)
```

✅ 출력 → `1 2`

🔙 백트래킹  
→ visited[1] = false

```text
i = 2 → 3 사용
→ output = [1, 3]
→ dfs(2)
```

✅ 출력 → `1 3`

🔙 visited[2] = false  
🔙 visited[0] = false

---

### 🔁 다음 루프 진행

```text
i = 1 → 2 사용
→ output = [2, _]
→ visited = [false, true, false]
→ dfs(1)
```

#### → i = 0 → 1 사용 → output = [2, 1]

✅ 출력 → `2 1`

#### → i = 2 → 3 사용 → output = [2, 3]

✅ 출력 → `2 3`

---

### 🔁 마지막 루프

```text
i = 2 → 3 사용
→ output = [3, _]
→ dfs(1)
```

#### → i = 0 → 1 사용 → [3, 1]

✅ 출력 → `3 1`

#### → i = 1 → 2 사용 → [3, 2]

✅ 출력 → `3 2`

---

## ✅ 최종 출력

```
1 2
1 3
2 1
2 3
3 1
3 2
```

---

## ✅ 정답 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Back_15654 {
    static int N, M;
    static int[] input, output;
    static boolean[] visited;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        input = new int[N];
        output = new int[M];
        visited = new boolean[N];

        st = new StringTokenizer(br.readLine());
        for(int i = 0; i < N; i++) input[i] = Integer.parseInt(st.nextToken());

        Arrays.sort(input); // 오름차순 정렬
        dfs(0);
        System.out.print(sb);
    }

    static void dfs(int depth) {
        if (depth == M) {
            for (int i = 0; i < M; i++) sb.append(output[i]).append(" ");
            sb.append("\n");
            return;
        }

        for (int i = 0; i < N; i++) {
            if (!visited[i]) {
                visited[i] = true;
                output[depth] = input[i];
                dfs(depth + 1);
                visited[i] = false;
            }
        }
    }
}
```

---

## 🧠 마무리 정리

| 항목          | 설명                               |
| ------------- | ---------------------------------- |
| DFS 기반      | 모든 순열 생성                     |
| visited       | 중복 방지를 위한 체크              |
| 오름차순 출력 | `Arrays.sort()` 사용               |
| 백트래킹      | 사용한 숫자 복원 후 다음 경우 탐색 |

---
