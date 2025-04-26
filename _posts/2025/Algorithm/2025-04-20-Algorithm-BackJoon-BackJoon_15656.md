---
published: true
title: "🔢 백준 15656번 - N과 M (7)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 15656번 문제에서 DFS 재귀 호출이 어떻게 작동하는지, 예제와 함께 완전히 시각화해서 정리합니다."
tag: "백준, 중복순열, DFS, 백트래킹, Java"
article_tag1: "중복순열"
article_section: "알고리즘"
meta_keywords: "백준 15656, 중복 순열, DFS 백트래킹, Java 순열, 사전순 출력"
last_modified_at: "2025-04-20 20:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🔢 백준 15656번 - N과 M (7)

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## ✅ 문제 요약

- N개의 자연수 중에서 **중복을 허용하여** M개를 고름
- 선택한 수열은 **사전 순으로 출력**
- 즉, **중복 순열 + 정렬된 출력**

![alt](/assets/images/post/Algorithm/15656_1.png)
![alt](/assets/images/post/Algorithm/15656_2.png)

---

## 📥 예제 입력

```
3 3
1231 1232 1233
```

- N = 3, M = 3
- 사용 가능한 숫자: `[1231, 1232, 1233]`

---

## 🎯 목표 출력

모든 중복 순열을 사전 순으로 출력:

```
1231 1231 1231
1231 1231 1232
1231 1231 1233
1231 1232 1231
...
1233 1233 1233
```

총 출력 개수: `3^3 = 27개`

---

## 🧠 DFS 로직 구조

```java
void dfs(int depth) {
    if (depth == M) {
        print(output);
        return;
    }

    for (int i = 0; i < N; i++) {
        output[depth] = input[i];
        dfs(depth + 1);
    }
}
```

- `depth`는 현재까지 선택한 숫자의 개수
- `output[depth]`에 값을 넣고, 다음 숫자를 선택
- `depth == M`이 되면 출력

---

## 🔍 DFS 흐름 예시

### 시작 상태

```text
depth = 0
output = [_, _, _]
```

---

### 깊이별 순회 구조 (트리처럼 생각)

```
depth = 0
├─ 1231 → dfs(1)
│   ├─ 1231 → dfs(2)
│   │   ├─ 1231 → dfs(3) → 출력: 1231 1231 1231
│   │   ├─ 1232 → dfs(3) → 출력: 1231 1231 1232
│   │   ├─ 1233 → dfs(3) → 출력: 1231 1231 1233
│   ├─ 1232 → dfs(2)
│   │   ├─ 1231 → 출력: 1231 1232 1231
│   │   ├─ 1232 → 출력: 1231 1232 1232
│   │   ├─ 1233 → 출력: 1231 1232 1233
│   ├─ 1233 → dfs(2)
│       ├─ 1231 → 출력: 1231 1233 1231
│       ├─ 1232 → 출력: 1231 1233 1232
│       ├─ 1233 → 출력: 1231 1233 1233
├─ 1232 → dfs(1)
│   ├─ ...
├─ 1233 → dfs(1)
    ├─ ...
```

---

## ✅ 최종 출력 결과 (총 27줄)

```
1231 1231 1231
1231 1231 1232
1231 1231 1233
1231 1232 1231
1231 1232 1232
1231 1232 1233
1231 1233 1231
1231 1233 1232
1231 1233 1233
1232 1231 1231
1232 1231 1232
1232 1231 1233
1232 1232 1231
1232 1232 1232
1232 1232 1233
1232 1233 1231
1232 1233 1232
1232 1233 1233
1233 1231 1231
1233 1231 1232
1233 1231 1233
1233 1232 1231
1233 1232 1232
1233 1232 1233
1233 1233 1231
1233 1233 1232
1233 1233 1233
```

---

## ✅ 핵심 포인트 요약

| 항목          | 설명                                 |
| ------------- | ------------------------------------ |
| 중복 허용     | ✅ 가능 (`1231 1231 1231`)           |
| 오름차순 출력 | ✅ 필요 (`Arrays.sort()` 사용)       |
| DFS 탐색 방식 | 매 depth마다 모든 input 반복         |
| 출력 개수     | N<sup>M</sup> = 3<sup>3</sup> = 27개 |

---

## ✅ 실제 사용 코드 (Java)

```java
import java.io.*;
import java.util.*;

public class Back_15656 {

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

        Arrays.sort(input); // 사전 순 출력을 위한 정렬

        dfs(0);

        System.out.print(sb);
    }

    static void dfs(int depth) {
        if (depth == M) {
            for (int i = 0; i < M; i++) {
                sb.append(output[i]).append(" ");
            }
            sb.append("\n");
            return;
        }

        for (int i = 0; i < N; i++) {
            output[depth] = input[i];
            dfs(depth + 1);
        }
    }
}
```

---
