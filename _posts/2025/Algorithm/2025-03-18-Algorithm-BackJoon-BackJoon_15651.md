---
published: true
title: "🔍 백준 15651번 - N과 M (3) (DFS/백트래킹)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - DFS
  - Backtracking
description: "백준 15651번 - N과 M (3) 문제의 DFS(백트래킹) 풀이 및 실행 과정 상세 분석"
tag: "DFS, 백트래킹, 중복 순열, Algorithm, Java"
article_tag1: "DFS"
article_section: "Algorithm"
meta_keywords: "백준, DFS, 백트래킹, 중복 순열, Algorithm, Java"
last_modified_at: "2025-03-17 17:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🔍 백준 15651번 - N과 M (3) (DFS/백트래킹)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

- **1부터 N까지의 자연수 중에서 M개를 중복하여 고르는 모든 경우**를 출력하는 문제입니다.
- 중복이 가능하기 때문에 **순열(Permutation)과 유사한 방식**으로 풀어야 합니다.
- 출력은 **사전순**으로 정렬되어야 합니다.

![alt](/assets/images/post/Algorithm/15651.png)

### ✅ **중복이 가능한 순열 (중복 순열)**

✔ **1부터 N까지의 수를 중복 허용하여 M개를 뽑아 나열**  
✔ **순서가 중요함 → 중복 순열(Permutation with Repetition)**  
✔ **DFS(백트래킹)를 활용하여 모든 경우의 수 탐색**

---

## **📌 2. 입력 및 출력 예시**

### **🔹 입력 예시**

```
3 2
```

### **🔹 출력 예시**

```
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

✅ **즉, 1~3까지의 수를 중복 포함하여 2개를 뽑는 모든 경우의 수 출력**

---

## **📌 3. DFS(백트래킹) 개념**

**DFS(백트래킹) 방식으로 모든 경우를 탐색하며 중복을 허용하는 구조**입니다.

- **M개의 숫자를 모두 채울 때까지 재귀 호출 진행**
- **각 자리에서 1부터 N까지 모든 숫자를 선택 가능 (중복 허용)**
- **StringBuilder를 활용하여 출력 최적화 (시간 초과 방지)**

---

## **📌 4. 코드 해설**

### **🔹 전체 코드**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_15651 {

    static int arr[];
    static int N;
    static int M;
    static StringBuilder sb = new StringBuilder(); // 최적화된 출력 처리

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken()); // 1~N까지의 자연수
        M = Integer.parseInt(st.nextToken()); // 뽑아야 할 개수

        arr = new int[M]; // 선택된 숫자를 저장할 배열
        dfs(0); // DFS 탐색 시작
        System.out.println(sb); // 결과 한 번에 출력
    }

    public static void dfs(int depth) {
        if (depth == M) { // M개를 모두 선택한 경우
            for (int i = 0; i < M; i++) {
                sb.append(arr[i]).append(" ");
            }
            sb.append('\n'); // 줄 바꿈 추가
            return;
        }

        for (int i = 1; i <= N; i++) { // 1부터 N까지 모든 숫자 선택 가능 (중복 O)
            arr[depth] = i; // 현재 위치(depth)에 숫자 저장
            dfs(depth + 1); // 다음 숫자 선택을 위해 재귀 호출
        }
    }
}
```

---

## **📌 5. `dfs()` 함수 상세 분석**

### **🔹 1️⃣ 기저 조건 (종료 조건)**

```java
if (depth == M) {
    for (int i = 0; i < M; i++) {
        sb.append(arr[i]).append(" ");
    }
    sb.append('\n');
    return;
}
```

✅ **설명**

- `depth == M`이면 **M개의 숫자를 다 뽑았으므로 출력 후 종료**
- `arr` 배열에 저장된 숫자들을 `sb.append()`로 저장 후 줄 바꿈 추가
- **재귀 종료 후 이전 단계로 되돌아감 (백트래킹)**

---

### **🔹 2️⃣ DFS 탐색 (재귀 호출)**

```java
for (int i = 1; i <= N; i++) { // 1부터 N까지 선택 가능 (중복 허용)
    arr[depth] = i;  // 현재 위치(depth)에 숫자 저장
    dfs(depth + 1);  // 다음 숫자 선택을 위해 재귀 호출
}
```

✅ **설명**

- `1`부터 `N`까지 **모든 숫자를 중복 허용하여 선택**
- `arr[depth] = i` → 현재 선택한 숫자를 `arr[]`에 저장
- `dfs(depth + 1)` → 다음 숫자를 선택하기 위해 재귀 호출

---

## **📌 6. DFS 실행 과정**

### ✅ **DFS 트리 형태**

```
dfs(0) ─────→ 1 선택 → dfs(1) ─────→ 1 선택 → dfs(2) → "1 1" 출력 후 백트래킹
                        │
                        ├──→ 2 선택 → dfs(2) → "1 2" 출력 후 백트래킹
                        │
                        ├──→ 3 선택 → dfs(2) → "1 3" 출력 후 백트래킹
                        │
dfs(0) ─────→ 2 선택 → dfs(1) ─────→ 1 선택 → dfs(2) → "2 1" 출력 후 백트래킹
                        │
                        ├──→ 2 선택 → dfs(2) → "2 2" 출력 후 백트래킹
                        │
                        ├──→ 3 선택 → dfs(2) → "2 3" 출력 후 백트래킹
                        │
dfs(0) ─────→ 3 선택 → dfs(1) ─────→ 1 선택 → dfs(2) → "3 1" 출력 후 백트래킹
                        │
                        ├──→ 2 선택 → dfs(2) → "3 2" 출력 후 백트래킹
                        │
                        ├──→ 3 선택 → dfs(2) → "3 3" 출력 후 백트래킹
```

✅ **설명**

1. `dfs(0)`에서 `1` 선택 → `dfs(1)` 호출
2. `dfs(1)`에서 `1` 선택 → `dfs(2)` 호출 → "1 1" 출력 후 `return`
3. `dfs(1)`에서 `2` 선택 → `dfs(2)` 호출 → "1 2" 출력 후 `return`
4. ... 반복하여 모든 경우 탐색

---

## **📌 7. 결론**

📌 **DFS(백트래킹)를 활용하여 "중복 가능"한 순열(중복 순열)을 생성하는 문제**  
📌 **출력 최적화를 위해 `StringBuilder`를 활용하여 빠른 실행 속도 유지**  
📌 **시간 복잡도는 `O(N^M)`이지만, N이 크지 않으므로 DFS로 충분히 해결 가능** 🚀

💡 **이제 "N과 M" 시리즈의 다른 문제도 쉽게 풀 수 있음!** 💪🔥  
📌 **이제 이걸 그대로 복사해서 블로그에 붙여넣으면 마크다운 형식으로 정리됩니다.** 🚀
