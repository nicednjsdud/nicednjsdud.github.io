---
published: true
title: "BackJoon 상범 빌딩 6593 (Java)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 6593번 상범 빌딩 문제(Java) 풀이"
tag: "BackJoon"
article_tag1: "Algorithm"
article_section: "Algorithm"
meta_keywords: "BackJoon,Algorithm,Java"
last_modified_at: "2025-02-24 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **📌 백준 6593번 - 상범 빌딩 (Java)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **💡 문제 설명**

3차원 빌딩에서 **탈출하는 최단 시간**을 구하는 문제입니다.  
탈출이 불가능하면 `"Trapped!"`을 출력하고, 가능하면 `"Escaped in X minute(s)."`을 출력합니다.

![alt](/assets/images/post/Algorithm/6593.png)

---

### **🔸 입력 예시**

```
3 4 5
S....
.###.
.##..
###.#
#####
##..E

1 3 3
S##
#E#
###

0 0 0
```

### **🔹 출력 예시**

```
Escaped in 11 minute(s).
Trapped!
```

---

## **📝 문제 풀이 핵심**

1. **BFS (너비 우선 탐색) 활용**
   - 3차원 공간에서 최단 거리 탐색 → **BFS가 적합**
   - `Queue<Node>`를 이용해 BFS 구현
2. **6가지 이동 방향** (동, 서, 남, 북, 위, 아래)
   - `static int[] dl, dr, dc`를 활용해 이동
3. **벽('#')은 이동 불가**, 방문 여부 체크 필요

---

## **💻 Java 코드**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_6593 {

    public static class Node {
        int l, r, c, count;

        public Node(int l, int r, int c, int count) {
            this.l = l;
            this.r = r;
            this.c = c;
            this.count = count;
        }
    }

    static int L, R, C;
    static int[] dl = {0, 0, 0, 0, 1, -1}; // 동 서 남 북 위 아래
    static int[] dr = {0, 0, -1, 1, 0, 0}; // 남 북
    static int[] dc = {1, -1, 0, 0, 0, 0}; // 동 서

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        while (true) {
            st = new StringTokenizer(br.readLine());

            L = Integer.parseInt(st.nextToken());
            R = Integer.parseInt(st.nextToken());
            C = Integer.parseInt(st.nextToken());
            if (L == 0 && R == 0 && C == 0) {
                break;
            }
            char[][][] building = new char[L][R][C];
            Node[] nodes = new Node[2]; // 시작점과 도착점 저장
            for (int i = 0; i < L; i++) {
                for (int j = 0; j < R; j++) {
                    String temp = br.readLine();
                    for (int k = 0; k < C; k++) {
                        char c = temp.charAt(k);
                        building[i][j][k] = c;
                        if (c == 'S') { // 시작 지점 입력
                            nodes[0] = new Node(i, j, k, 0);
                        } else if (c == 'E') { // 도착 지점 입력
                            nodes[1] = new Node(i, j, k, 0);
                        }
                    }
                }
                String blank = br.readLine();
            }

            int result = bfs(nodes, building);
            if (result == -1) {
                System.out.println("Trapped!");
            } else {
                System.out.println("Escaped in " + result + " minute(s).");
            }
        }
        br.close();
    }

    private static int bfs(Node[] nodes, char[][][] building) {
        Queue<Node> q = new LinkedList<>();
        q.offer(nodes[0]);

        boolean visited[][][] = new boolean[L][R][C];
        visited[nodes[0].l][nodes[0].r][nodes[0].c] = true; // 시작 위치 방문 처리

        while (!q.isEmpty()) {
            Node node = q.poll();
            // 목표 지점에 도달하면 이동 횟수 반환
            if (node.l == nodes[1].l && node.r == nodes[1].r && node.c == nodes[1].c) {
                return node.count;
            }

            for(int i = 0; i< 6; i++){
                int curL = node.l + dl[i];
                int curR = node.r + dr[i];
                int curC = node.c + dc[i];

                if(curL >= 0 && curL < L
                        && curR >= 0 && curR < R
                        && curC >= 0 && curC < C
                ){
                    if(!visited[curL][curR][curC] && building[curL][curR][curC] != '#') {
                        visited[curL][curR][curC] = true;
                        q.offer(new Node(curL, curR, curC, node.count + 1));
                    }
                }
            }
        }
        return -1;
    }
}
```

---

## **🚨 오류 원인: `dr` 배열의 값 변경**

```java
// 기존 코드 (정상 동작)
static int[] dr = {0, 0, -1, 1, 0, 0}; // 남 북

// 오류가 발생한 코드
static int[] dr = {0, 0, 1, -1, 0, 0}; // 북 남
```

### **🔹 원인**

- `dr` 배열에서 **남(아래)** 방향과 **북(위)** 방향이 **뒤바뀜**
- `dr = {0, 0, -1, 1, 0, 0};` → `(-1, 1)` 순서로 되어 있어야 하는데  
  `dr = {0, 0, 1, -1, 0, 0};`로 바뀌면 **반대 방향으로 이동**

### **🔹 결과**

- BFS 탐색 시, **반대로 이동하여 경로를 찾지 못하는 오류 발생**
- **예상 경로와 다른 방향으로 이동하여 탈출이 불가능해짐**

---

## **📢 결론**

✅ `-1`은 **위쪽**, `1`은 **아래쪽**을 의미해야 함  
✅ 방향 설정을 잘못하면 BFS 경로 탐색이 **완전히 달라짐**  
✅ **이동 방향을 바꿀 때 반드시 주석을 확인하고 신중히 수정해야 함!**

---

### **🖋️ 더 좋은 풀이 방법이 있다면 댓글로 알려주세요! 😊**
