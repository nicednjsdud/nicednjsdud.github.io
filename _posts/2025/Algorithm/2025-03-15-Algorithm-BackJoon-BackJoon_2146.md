---
published: true
title: "🌉 백준 2146번 다리 만들기 (BFS 풀이)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - BFS
description: "백준 2146번 다리 만들기 (BFS)를 활용한 최단 다리 찾기 문제 해결"
tag: "BFS, Java, Algorithm, Queue, 다리 만들기"
article_tag1: "BFS"
article_section: "Algorithm"
meta_keywords: "BFS, Java, Algorithm, Queue, 다리 만들기, 백준, BOJ 2146"
last_modified_at: "2025-02-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🌉 백준 2146번 - 다리 만들기 (BFS 풀이)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

N×N 크기의 지도에서 여러 개의 섬이 존재하며,  
각 섬을 연결하는 가장 짧은 다리(`0`으로만 이루어진 바다)를 찾아야 합니다.  
단, 다리는 직선으로만 연결 가능하고, 대각선 이동은 허용되지 않습니다.

![alt](/assets/images/post/Algorithm/2146_1.png)
![alt](/assets/images/post/Algorithm/2146_2.png)

---

## **📌 2. 입력 및 출력 예시**

### **🔹 입력 예시**

```
10
1 1 1 0 0 0 0 1 1 1
1 1 1 0 0 0 0 1 1 1
1 1 1 0 0 0 0 0 1 1
0 0 0 0 0 0 0 0 1 1
0 0 0 0 0 0 0 0 1 1
0 0 0 0 0 0 0 0 1 1
1 1 0 0 0 0 0 0 1 1
1 1 1 0 0 0 0 1 1 1
1 1 1 0 0 0 0 1 1 1
1 1 1 0 0 0 0 1 1 1
```

### **🔹 출력 예시**

```
3
```

📌 **설명**

- 가장 짧은 다리는 길이가 `3`입니다.

---

## **📌 3. 해결 방법 (BFS)**

이 문제는 **최단 거리 문제**이므로  
**BFS(너비 우선 탐색, Breadth-First Search)**를 사용해야 합니다.

### **🔹 BFS를 사용해야 하는 이유**

- **최단 거리 탐색**이므로 **BFS가 적합**
- DFS를 사용하면 **모든 경로를 탐색해야 하므로 비효율적**
- BFS는 **각 섬을 탐색하면서 가장 짧은 거리의 다리를 찾을 수 있음**

---

## **📌 4. 핵심 코드 분석**

### **🔹 섬을 구분하는 BFS (각 섬에 고유한 번호 부여)**

```java
private static void markIsland(int x, int y, int islandNumber) {
    Queue<Point> q = new LinkedList<>();
    q.offer(new Point(x, y, 0, islandNumber));
    visited[x][y] = true;
    map[x][y] = islandNumber;

    while (!q.isEmpty()) {
        Point now = q.poll();

        for (int i = 0; i < 4; i++) {
            int nx = now.x + dX[i];
            int ny = now.y + dY[i];

            if (nx >= 0 && ny >= 0 && nx < N && ny < N) {
                if (!visited[nx][ny] && map[nx][ny] == 1) {
                    visited[nx][ny] = true;
                    map[nx][ny] = islandNumber;
                    q.offer(new Point(nx, ny, 0, islandNumber));
                }
            }
        }
    }
}
```

✅ **설명**

- `markIsland()`는 BFS를 사용하여 **각 섬을 탐색**하며 `islandNumber`를 할당
- **같은 섬에 속하는 모든 점을 같은 번호로 표시**

---

### **🔹 다리 찾기 (BFS)**

```java
private static void findShortestBridge() {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (map[i][j] > 1) { // 섬이 존재하는 위치라면
                boolean[][] visited = new boolean[N][N];
                bfs(i, j, map[i][j], visited);
            }
        }
    }
}
```

✅ **설명**

- `findShortestBridge()`는 **모든 섬에서 BFS 탐색을 수행**하여 최단 다리를 찾음

---

### **🔹 BFS로 다리 길이 계산**

```java
private static void bfs(int x, int y, int islandNumber, boolean[][] visited) {
    Queue<Point> q = new LinkedList<>();
    q.offer(new Point(x, y, 0, islandNumber));
    visited[x][y] = true;

    while (!q.isEmpty()) {
        Point now = q.poll();

        for (int i = 0; i < 4; i++) {
            int nx = now.x + dX[i];
            int ny = now.y + dY[i];

            if (nx >= 0 && ny >= 0 && nx < N && ny < N && !visited[nx][ny]) {
                if (map[nx][ny] == 0) { // 바다인 경우
                    visited[nx][ny] = true;
                    q.offer(new Point(nx, ny, now.count + 1, islandNumber));
                } else if (map[nx][ny] != islandNumber) { // 다른 섬에 도착
                    min = Math.min(min, now.count);
                    return;
                }
            }
        }
    }
}
```

✅ **설명**

- BFS를 사용하여 **다리를 확장**하면서 **가장 먼저 도착하는 다리의 길이를 기록**
- **다른 섬에 도착하면 현재 `count` 값을 `min`과 비교**하여 최소값을 저장

---

## **📌 5. 전체 코드 (최종 수정)**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_2146 {

    static class Point {
        int x, y, count, island;

        public Point(int x, int y, int count, int island) {
            this.x = x;
            this.y = y;
            this.count = count;
            this.island = island;
        }
    }

    static int[] dX = {0, 0, 1, -1};
    static int[] dY = {1, -1, 0, 0};

    static int[][] map;
    static boolean[][] visited;
    static int N, min = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        map = new int[N][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int islandNumber = 2;
        visited = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 1 && !visited[i][j]) {
                    markIsland(i, j, islandNumber);
                    islandNumber++;
                }
            }
        }

        findShortestBridge();
        System.out.println(min);
    }
}
```

---

## **📌 6. 결론**

🚀 **BFS로 각 섬을 탐색하여 구분한 후, 최단 거리의 다리를 찾는 방식으로 해결**  
🏆 **시간 복잡도: `O(N²)`, 즉 N이 커도 빠르게 실행 가능!**  
🔥 **이제 올바르게 동작할 것이며, 최단 거리 다리를 찾을 수 있음!**
