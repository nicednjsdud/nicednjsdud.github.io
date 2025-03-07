---
published: true
title: "🔥 백준 5472번 불! (BFS 풀이 및 오류 분석)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
  - BFS
description: "백준 5472번 불! (BFS)를 활용한 최단 시간 탈출 문제 해결 및 오류 분석"
tag: "BFS, Java, Algorithm, Queue, Fire Escape"
article_tag1: "BFS"
article_section: "Algorithm"
meta_keywords: "BFS, Java, Algorithm, Queue, Fire Escape, 백준, BOJ 5472"
last_modified_at: "2025-03-06 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🔥 백준 5472번 - 불! (BFS 풀이 및 오류 분석)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

상근(`@`)이가 불(`*`)이 번지는 건물에서 탈출하는 문제입니다.  
불(`*`)은 **동시에 퍼지고**, 상근(`@`)이는 **한 칸씩 이동**할 수 있습니다.  
**벽(`#`)은 이동할 수 없고**, 상근이가 **건물의 가장자리**에 도달하면 탈출할 수 있습니다.

![alt](/assets/images/post/Algorithm/5472_1.png)
![alt](/assets/images/post/Algorithm/5472_2.png)

---

## **📌 2. 입력 및 출력 예시**

### **🔹 입력 예시**

```
3
4 3
####
#*@#
####
7 6
###.###
#*#.#*#
#.....#
#.....#
#..@..#
#######
7 4
###.###
#*#.#*#
#.....#
####@##
```

### **🔹 출력 예시**

```
IMPOSSIBLE
5
IMPOSSIBLE
```

📌 **설명**

- `@`(상근)는 이동하면서 탈출을 시도
- `*`(불)은 **동시에 확산**되며 상근의 이동을 방해
- **탈출이 가능하면 최소 시간 출력, 불가능하면 "IMPOSSIBLE" 출력**

---

## **📌 3. 해결 방법 (BFS)**

이 문제는 **최단 경로 탐색 문제**이므로,  
**BFS(너비 우선 탐색, Breadth-First Search)**를 사용해야 합니다.

### **🔹 핵심 로직**

1. **불(`*`)과 상근(`@`)을 각각 BFS 큐에 저장**
2. **불(`*`)이 먼저 확산**, 그 후 **상근(`@`)이 이동**
3. **상근(`@`)이 건물의 가장자리에 도달하면 즉시 탈출**
4. **상근(`@`)이 이동할 곳이 없으면 "IMPOSSIBLE" 출력**

---

## **📌 4. 오류 분석 및 해결**

### **🔹 오류 1: 잘못된 배열 범위 검사**

```java
if (nx < 0 || ny < 0 || nx >= width || ny >= height) {
    continue;
}
```

✅ **문제점:**

- `nx`와 `ny`는 **행(row)**, **열(column)**을 나타냄
- **올바른 범위 검사는 `nx >= height` / `ny >= width`**가 되어야 함

✅ **해결 방법:**

```java
if (nx < 0 || ny < 0 || nx >= height || ny >= width) {
    continue;
}
```

---

### **🔹 오류 2: BFS에서 `sangQ.poll()`을 한 번만 호출하는 문제**

```java
Point sang = sangQ.poll();
```

✅ **문제점:**

- **현재 코드에서는 `sangQ.poll()`이 한 번만 호출되므로, 한 번의 BFS 루프에서 상근(`@`)이 한 칸씩만 이동함**
- **반면 불(`*`)은 여러 개가 동시에 확산하므로, 상근이가 불을 피하지 못하는 문제가 발생**

✅ **해결 방법:**  
🚀 **BFS의 "레벨 단위"로 이동하도록 `sangSize` 적용**

```java
int sangSize = sangQ.size();
for (int s = 0; s < sangSize; s++) {
    Point sang = sangQ.poll();
    // 이동 처리
}
```

---

### **🔹 오류 3: `visited` 좌표 체계 오류**

```java
if (map[nextY][nextX] == '.' && visited[nextY][nextX] == 0) {
```

✅ **문제점:**

- **배열 좌표 체계(`map[nextY][nextX]`)에서 `nextX`와 `nextY`가 반대로 들어감**
- **`map[y][x]` 형태로 접근해야 함**

✅ **해결 방법:**  
🚀 올바른 좌표 체계 적용

```java
if (map[nextRow][nextCol] == '.' && visited[nextRow][nextCol] == 0) {
```

---

## **📌 5. 수정된 코드**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_5472 {

    static class Point {
        int x, y, time;
        Point(int x, int y, int time) {
            this.x = x;
            this.y = y;
            this.time = time;
        }
    }

    static int[] dX = {0, 0, 1, -1}; // 이동 방향 (좌우)
    static int[] dY = {1, -1, 0, 0}; // 이동 방향 (상하)

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine());

        StringTokenizer st;
        for (int i = 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            int w = Integer.parseInt(st.nextToken());
            int h = Integer.parseInt(st.nextToken());

            char[][] map = new char[h][w];

            Queue<Point> fires = new LinkedList<>();
            Queue<Point> sang = new LinkedList<>();

            for (int j = 0; j < h; j++) {
                String temp = br.readLine();
                for (int k = 0; k < w; k++) {
                    map[j][k] = temp.charAt(k);

                    if (map[j][k] == '*') {
                        fires.offer(new Point(j, k, 0));
                    } else if (map[j][k] == '@') {
                        sang.offer(new Point(j, k, 0));
                    }
                }
            }
            int result = bfs(w, h, map, sang, fires);
            System.out.println(result == -1 ? "IMPOSSIBLE" : result);
        }
    }

    private static int bfs(int width, int height, char[][] map, Queue<Point> sangQ, Queue<Point> fires) {
        int[][] visited = new int[height][width];

        while (!sangQ.isEmpty()) {

            // 🔥 불 확산
            int fireSize = fires.size();
            for (int f = 0; f < fireSize; f++) {
                Point fire = fires.poll();
                for (int i = 0; i < 4; i++) {
                    int nx = fire.x + dX[i];
                    int ny = fire.y + dY[i];

                    if (nx < 0 || ny < 0 || nx >= height || ny >= width) {
                        continue;
                    }

                    if (map[nx][ny] == '.' || map[nx][ny] == '@') {
                        map[nx][ny] = '*';
                        fires.offer(new Point(nx, ny, fire.time + 1));
                    }
                }
            }

            // 🏃‍♂️ 상근 이동 (레벨 BFS)
            int sangSize = sangQ.size();
            for (int s = 0; s < sangSize; s++) {
                Point sang = sangQ.poll();
                for (int i = 0; i < 4; i++) {
                    int nextRow = sang.x + dX[i];
                    int nextCol = sang.y + dY[i];

                    if (nextRow < 0 || nextCol < 0 || nextRow >= height || nextCol >= width) {
                        return sang.time + 1;
                    }

                    if (map[nextRow][nextCol] == '.' && visited[nextRow][nextCol] == 0) {
                        visited[nextRow][nextCol] = 1;
                        sangQ.offer(new Point(nextRow, nextCol, sang.time + 1));
                    }
                }
            }
        }
        return -1;
    }
}
```

---

**💡 더 나은 방법이 있다면 댓글로 공유해주세요! 😊**
