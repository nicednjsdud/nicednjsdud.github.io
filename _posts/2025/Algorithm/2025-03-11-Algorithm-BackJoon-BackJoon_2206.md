---
published: true
title: "🧱 백준 2206번 벽 부수고 이동하기 (BFS 풀이)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - BFS
description: "백준 2206번 벽 부수고 이동하기 (BFS)를 활용한 최단 거리 탐색"
tag: "BFS, Java, Algorithm, Queue, 벽 부수고 이동"
article_tag1: "BFS"
article_section: "Algorithm"
meta_keywords: "BFS, Java, Algorithm, Queue, 벽 부수고 이동, 백준, BOJ 2206"
last_modified_at: "2025-02-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🧱 백준 2206번 - 벽 부수고 이동하기 (BFS 풀이)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

N×M 크기의 배열이 주어지고,  
벽(`1`)이 있는 경우 **한 개의 벽을 부수고 지나갈 수 있다**.  
최단 거리로 도착점 `(N-1, M-1)`까지 이동해야 한다.

![alt](/assets/images/post/Algorithm/2206_1.png)
![alt](/assets/images/post/Algorithm/2206_2.png)

---

## **📌 2. 입력 및 출력 예시**

### **🔹 입력 예시**

```
6 4
0100
1110
1000
0000
0111
0000
```

### **🔹 출력 예시**

```
15
```

📌 **설명**

- `(0,0)`에서 `(5,3)`까지 최단 거리로 이동
- 벽을 한 번 부수는 경우 더 빠른 경로 가능

---

## **📌 3. 해결 방법 (BFS)**

이 문제는 **최단 경로 문제**이므로  
**BFS(너비 우선 탐색, Breadth-First Search)**를 사용해야 한다.

### **🔹 BFS를 사용해야 하는 이유**

- 모든 칸을 한 번씩 방문하는 경우 **O(N×M)**
- DFS(깊이 우선 탐색)보다 **BFS가 최단 거리 탐색에 적합**
- BFS를 활용하여 **벽을 한 번만 부술 수 있도록 관리**

---

## **📌 4. 핵심 코드 분석**

```java
static class Point {
    int x, y, count;
    boolean destroyed; // 벽을 부쉈는지 여부

    public Point(int x, int y, int count, boolean destroyed) {
        this.x = x;
        this.y = y;
        this.count = count;
        this.destroyed = destroyed;
    }
}
```

✅ **`Point` 클래스**

- `x`, `y` → 현재 좌표
- `count` → 이동 거리 (최단 거리)
- `destroyed` → 벽을 부쉈는지 여부 (`true` = 부숨)

---

### **🔹 `visited` 3차원 배열 (벽을 부순 경우 vs 부수지 않은 경우)**

```java
boolean[][][] visited = new boolean[N][M][2];
```

✅ **`visited[N][M][0]`** → 벽을 부수지 않고 방문한 경우  
✅ **`visited[N][M][1]`** → 벽을 부순 후 방문한 경우  
✅ 같은 위치를 **벽을 부순 상태/부수지 않은 상태로 방문할 수 있으므로 3차원 배열을 사용**

---

### **🔹 BFS 탐색 과정**

```java
Queue<Point> points = new LinkedList<>();
points.offer(new Point(0, 0, 1, false));
visited[0][0][0] = true;
```

✅ **BFS를 위한 큐 초기화**

- `(0,0)`에서 시작 (`count=1`)
- 처음에는 벽을 부수지 않은 상태 (`destroyed=false`)

---

### **🔹 BFS 탐색 (벽 부수기 로직 포함)**

```java
for (int i = 0; i < 4; i++) {
    int dirX = now.x + dX[i];
    int dirY = now.y + dY[i];

    if (dirX >= N || dirX < 0 || dirY >= M || dirY < 0) continue;

    // 이동 가능 (빈 공간)
    if (map[dirX][dirY] == '0') {
        if (!now.destroyed && !visited[dirX][dirY][0]) {
            points.offer(new Point(dirX, dirY, now.count + 1, false));
            visited[dirX][dirY][0] = true;
        } else if (now.destroyed && !visited[dirX][dirY][1]) {
            points.offer(new Point(dirX, dirY, now.count + 1, true));
            visited[dirX][dirY][1] = true;
        }
    }

    // 벽 부수기 (벽을 한 번도 부수지 않은 경우)
    else if (map[dirX][dirY] == '1') {
        if (!now.destroyed) {
            points.offer(new Point(dirX, dirY, now.count + 1, true));
            visited[dirX][dirY][1] = true;
        }
    }
}
```

✅ **이동할 수 있는 경우**

- **빈 공간(`0`)일 때** → 벽을 부순 여부에 따라 방문 체크
- **벽(`1`)을 부술 수 있는 경우** → 한 번만 부수도록 설정

---

### **🔹 목표 지점 도착 여부 확인**

```java
if (now.x == N - 1 && now.y == M - 1) {
    return now.count;
}
```

✅ **도착하면 즉시 최단 거리 반환**  
✅ BFS는 **최단 거리를 보장하므로**, 첫 번째 도착한 경로가 항상 최단 거리

---

## **📌 5. 전체 코드 (최종 수정)**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_2206 {

    static class Point {
        int x, y, count;
        boolean destroyed;

        public Point(int x, int y, int count, boolean destroyed) {
            this.x = x;
            this.y = y;
            this.count = count;
            this.destroyed = destroyed;
        }
    }

    static int[] dX = {0, 0, 1, -1};
    static int[] dY = {1, -1, 0, 0};

    static int N, M;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        char[][] map = new char[N][M];

        for (int i = 0; i < N; i++) {
            String temp = br.readLine();
            for (int j = 0; j < M; j++) {
                map[i][j] = temp.charAt(j);
            }
        }
        System.out.println(bfs(map));
    }

    private static int bfs(char[][] map) {
        Queue<Point> points = new LinkedList<>();
        points.offer(new Point(0, 0, 1, false));
        boolean[][][] visited = new boolean[N][M][2];

        visited[0][0][0] = true;
        while (!points.isEmpty()) {
            Point now = points.poll();

            if (now.x == N - 1 && now.y == M - 1) {
                return now.count;
            }

            for (int i = 0; i < 4; i++) {
                int dirX = now.x + dX[i];
                int dirY = now.y + dY[i];

                if (dirX >= N || dirX < 0 || dirY >= M || dirY < 0) continue;
```
