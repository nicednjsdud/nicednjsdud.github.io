---
published: true
title: "🔥 백준 4179번 불! (BFS 풀이)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 4179번 불! (BFS)를 활용한 최단 시간 탈출 문제 해결"
tag: "BFS, Java, Algorithm, Queue, Fire Escape"
article_tag1: "BFS"
article_section: "Algorithm"
meta_keywords: "BFS, Java, Algorithm, Queue, Fire Escape, 백준, BOJ 4179"
last_modified_at: "2025-03-05 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🔥 백준 4179번 - 불! (BFS 풀이)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **📌 1. 문제 설명**

지훈(`J`)이가 불(`F`)이 난 미로에서 탈출하는 문제입니다.  
불(`F`)은 **동시에 퍼지고**, 지훈(`J`)이는 **한 칸씩 이동**할 수 있습니다.  
**벽(`#`)은 이동할 수 없고**, 지훈이가 **미로의 가장자리**에 도달하면 탈출할 수 있습니다.

![alt](/assets/images/post/Algorithm/4179.png)

---

## **📌 2. 입력 및 출력 예시**

### **🔹 입력 예시**

```
4 4
####
#JF#
#..#
#..#
```

### **🔹 출력 예시**

```
3
```

📌 **설명**

- `J`(지훈)는 (1,2)에서 시작
- `F`(불)는 (1,1)에서 시작
- 불은 **동시에 확산**되고, 지훈이는 불보다 먼저 도착하면 탈출 가능

---

## **📌 3. 해결 방법 (BFS)**

이 문제는 **최단 경로 탐색 문제**이므로,  
**BFS(너비 우선 탐색, Breadth-First Search)**를 사용해야 합니다.

### **🔹 핵심 로직**

1. **불(`F`)과 지훈(`J`)을 각각 BFS 큐에 저장**
2. **불(`F`)이 먼저 확산**, 그 후 **지훈(`J`)이 이동**
3. **지훈(`J`)이 미로의 가장자리에 도달하면 즉시 탈출**
4. **지훈(`J`)이 이동할 곳이 없으면 "IMPOSSIBLE" 출력**

---

## **📌 4. Java 코드 (BFS)**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Back_4179 {

    static int dX[] = {0, 0, 1, -1};
    static int dY[] = {1, -1, 0, 0};

    static int R, C;

    static class Point {
        int x, y, time;

        Point(int x, int y, int time) {
            this.x = x;
            this.y = y;
            this.time = time;
        }
    }

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        char[][] map = new char[R][C];
        Queue<Point> fires = new LinkedList<>();
        Queue<Point> jihos = new LinkedList<>();

        for (int i = 0; i < R; i++) {
            String temp = br.readLine();
            for (int j = 0; j < C; j++) {
                map[i][j] = temp.charAt(j);
                if (map[i][j] == 'F') {
                    fires.offer(new Point(i, j, 0)); // 불 위치 저장
                } else if (map[i][j] == 'J') {
                    jihos.offer(new Point(i, j, 0)); // 지훈 위치 저장
                }
            }
        }

        int result = bfs(map, jihos, fires);
        System.out.println(result == -1 ? "IMPOSSIBLE" : result);
    }

    private static int bfs(char[][] map, Queue<Point> jihos, Queue<Point> fires) {
        int[][] visited = new int[R][C];

        while (!jihos.isEmpty()) {
            // 🔥 불 확산
            int fireSize = fires.size();
            for (int f = 0; f < fireSize; f++) {
                Point fire = fires.poll();
                for (int i = 0; i < 4; i++) {
                    int nx = fire.x + dX[i];
                    int ny = fire.y + dY[i];

                    if (nx < 0 || ny < 0 || nx >= R || ny >= C) {
                        continue;
                    }

                    if (map[nx][ny] == '.' || map[nx][ny] == 'J') {
                        map[nx][ny] = 'F';
                        fires.offer(new Point(nx, ny, fire.time + 1));
                    }
                }
            }

            // 🏃‍♂️ 지훈 이동
            int jihoSize = jihos.size();
            for (int j = 0; j < jihoSize; j++) {
                Point jiho = jihos.poll();
                for (int i = 0; i < 4; i++) {
                    int nx = jiho.x + dX[i];
                    int ny = jiho.y + dY[i];

                    // ✅ 가장자리에 도달하면 탈출
                    if (nx < 0 || ny < 0 || nx >= R || ny >= C) {
                        return jiho.time + 1;
                    }

                    if (map[nx][ny] == '.' && visited[nx][ny] == 0) {
                        visited[nx][ny] = 1;
                        jihos.offer(new Point(nx, ny, jiho.time + 1));
                    }
                }
            }
        }
        return -1;
    }
}
```

---

## **📌 5. 핵심 코드 설명**

### **1️⃣ `fires` 큐를 사용하여 불(`F`) 확산**

```java
int fireSize = fires.size();
for (int f = 0; f < fireSize; f++) {
    Point fire = fires.poll();
    for (int i = 0; i < 4; i++) {
        int nx = fire.x + dX[i];
        int ny = fire.y + dY[i];

        if (nx < 0 || ny < 0 || nx >= R || ny >= C) {
            continue;
        }

        if (map[nx][ny] == '.' || map[nx][ny] == 'J') {
            map[nx][ny] = 'F';
            fires.offer(new Point(nx, ny, fire.time + 1));
        }
    }
}
```

✅ **한 번의 BFS 단계에서 모든 불을 확산시킴**  
✅ **불(`F`)이 먼저 이동하도록 하여 지훈(`J`)의 이동을 방해하도록 설정**

---

### **2️⃣ `jihos` 큐를 사용하여 지훈(`J`) 이동**

```java
int jihoSize = jihos.size();
for (int j = 0; j < jihoSize; j++) {
    Point jiho = jihos.poll();
    for (int i = 0; i < 4; i++) {
        int nx = jiho.x + dX[i];
        int ny = jiho.y + dY[i];

        if (nx < 0 || ny < 0 || nx >= R || ny >= C) {
            return jiho.time + 1;
        }

        if (map[nx][ny] == '.' && visited[nx][ny] == 0) {
            visited[nx][ny] = 1;
            jihos.offer(new Point(nx, ny, jiho.time + 1));
        }
    }
}
```

✅ **불보다 먼저 도착하면 탈출 성공!**  
✅ **불(`F`)과 지훈(`J`)이 같은 시간대에 확산되는 구조**

---

## **📌 6. 결론**

✅ **BFS를 활용하여 최단 시간으로 탈출 경로를 찾음**  
✅ **불(`F`)이 먼저 확산되도록 하여, 지훈(`J`)이 지나갈 길을 막음**  
✅ **지훈(`J`)이 가장자리에 도달하면 탈출 성공!**

---

\*\*💡 더 나은 방법이 있다면 댓글
