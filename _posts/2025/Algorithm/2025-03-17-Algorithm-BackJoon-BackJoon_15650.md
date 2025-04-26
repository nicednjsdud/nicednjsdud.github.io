---
published: true
title: "📝 백준 15650번 - N과 M (2) (DFS/백트래킹)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 15650번 - N과 M (2) 문제의 DFS(백트래킹) 풀이 및 핵심 개념 정리"
tag: "DFS, 백트래킹, 조합, Algorithm, Java"
article_tag1: "DFS"
article_section: "Algorithm"
meta_keywords: "백준, DFS, 백트래킹, 조합, Algorithm, Java"
last_modified_at: "2025-03-17 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **📝 백준 15650번 - N과 M (2) (DFS/백트래킹)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

자연수 **N과 M**이 주어졌을 때,  
**1부터 N까지의 수 중에서 중복 없이 M개를 고르는 문제**입니다.  
단, **고른 수열은 오름차순이어야 합니다.**

📌 **즉, 조합(combination) 개념을 활용해야 하는 문제!**  
✔ **순서 상관 없음 (조합)**  
✔ **중복 허용 안됨**  
✔ **오름차순 정렬 필수**

![alt](/assets/images/post/Algorithm/15650.png)

---

## **📌 2. 입력 및 출력 예시**

### **입력 예시**

```
4 2
```

### **출력 예시**

```
1 2
1 3
1 4
2 3
2 4
3 4
```

📌 **즉, 1부터 4까지의 수에서 2개를 고르는 조합을 출력하는 문제!**

---

## **📌 3. 해결 방법 (DFS)**

**이 문제는 "조합(Combination)"을 구하는 문제이므로 DFS(백트래킹) 방식으로 해결할 수 있습니다.**  
우리는 **중복을 방지하고, 오름차순을 유지**해야 하므로, `dfs()`에서 **start 변수를 활용**하여 중복 없이 숫자를 선택합니다.

### ✅ **DFS를 활용한 핵심 아이디어**

- `arr[]` 배열을 사용하여 M개의 숫자를 저장
- `dfs(start, depth)`를 호출하면서 현재 선택한 숫자(`depth`)를 증가
- **중복 방지**를 위해 `start`를 다음 숫자로 설정 (`i + 1`)

---

## **📌 4. 핵심 코드 해설**

### **🔹 DFS 재귀함수**

```java
private static void dfs(int start, int depth) {
    // M개를 선택한 경우 출력
    if (depth == M) {
        for (int i : arr)
            System.out.print(i + " ");
        System.out.println();
        return;
    }

    // start부터 N까지 숫자 선택 (오름차순 유지)
    for (int i = start; i <= N; i++) {
        arr[depth] = i;  // 현재 위치에 숫자 저장
        dfs(i + 1, depth + 1);  // 다음 숫자로 이동
    }
}
```

✅ **설명**

- **기저 조건**: `depth == M`이면 조합을 완성한 것이므로 출력
- **for문을 활용해 숫자 선택** (`start`부터 `N`까지)
- **중복 방지**: `dfs(i + 1, depth + 1)` → 현재 선택한 숫자 이후부터 탐색

---

### **🔹 전체 코드 정리**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_15650 {

    public static int[] arr;
    public static int N, M;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        arr = new int[M];

        dfs(1, 0);  // 1부터 시작, depth는 0
    }

    private static void dfs(int start, int depth) {
        if (depth == M) {
            for (int i : arr)
                System.out.print(i + " ");
            System.out.println();
            return;
        }

        for (int i = start; i <= N; i++) {
            arr[depth] = i;  // 현재 위치에 숫자 저장
            dfs(i + 1, depth + 1);  // 다음 숫자로 이동 (중복 방지)
        }
    }
}
```

---

## **📌 5. 핵심 정리**

✅ **DFS(백트래킹)로 "조합(Combination)"을 구하는 문제**  
✅ **`start` 변수를 사용하여 중복을 방지하고, 오름차순을 유지**  
✅ **`dfs(start, depth)`**에서 `start`를 증가(`i + 1`)하여 이전 숫자보다 작은 숫자를 선택하지 않도록 설정  
✅ **기저 조건**: `depth == M`이면 조합을 완성한 것이므로 출력

---

## **📌 6. 시간 복잡도 분석**

**이 문제의 시간 복잡도는 조합의 개수와 동일합니다.**  
✔ **N개의 숫자 중 M개를 선택하는 경우의 수** → **O( C(N, M) )**  
✔ 조합의 공식:  
\[
C(N, M) = \frac{N!}{M!(N-M)!}
\]
✔ **예시** (`N=4, M=2`)
\[
C(4, 2) = \frac{4!}{2!(4-2)!} = \frac{4 \times 3}{2 \times 1} = 6
\]
✔ 즉, **N이 크더라도 DFS 방식으로 충분히 빠르게 해결 가능!** 🚀

---

## **📌 7. 결론**

📌 **DFS 백트래킹을 활용하여 "중복 없이, 오름차순"으로 조합을 생성하는 문제**  
📌 **start 변수를 활용하여 중복을 방지하고, 조합의 순서를 유지하는 것이 핵심**  
📌 **시간 복잡도는 O(C(N, M))이며, N이 크지 않으므로 DFS로 충분히 해결 가능** 🚀

**💡 백트래킹 문제를 연습하는 데 아주 좋은 문제! 😊**  
📌 **이제 이걸 이해하면 N과 M (1) ~ (4) 시리즈 문제도 쉽게 풀 수 있을 거야!** 💪🔥  
📌 **이제 이걸 그대로 복사해서 블로그에 붙여넣으면 마크다운 형식으로 정리됩니다.** 🚀
