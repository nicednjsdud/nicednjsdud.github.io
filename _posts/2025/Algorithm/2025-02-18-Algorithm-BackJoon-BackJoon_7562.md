---
published: true
title: BackJoon 나이트의 이동 7562 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 나이트의 이동 7562 (Java)
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2025-02-18 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/7562.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_7562_2 {

    // 나이트가 이동할 수 있는 8가지 방향
    static int[] dX = {1, 2, 2, 1, -1, -2, -2, -1};
    static int[] dY = {2, 1, -1, -2, -2, -1, 1, 2};

    // 좌표 및 이동 횟수를 저장하는 클래스
    static class Point {
        int x;
        int y;
        int count;

        public Point(int x, int y, int count) {
            this.x = x;
            this.y = y;
            this.count = count;  // 현재까지 이동한 횟수 저장
        }
    }

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine()); // 테스트 케이스 개수 입력

        for (int i = 0; i < T; i++) {
            int I = Integer.parseInt(br.readLine()); // 체스판 크기 (I x I)
            Point[] points = new Point[2]; // 시작점과 도착점 저장

            // 시작점과 도착점 입력
            for (int j = 0; j < 2; j++) {
                st = new StringTokenizer(br.readLine());
                int start = Integer.parseInt(st.nextToken());
                int end = Integer.parseInt(st.nextToken());
                points[j] = new Point(start, end, 0);
            }

            // BFS 실행 및 결과 출력
            System.out.println(bfs(points, I));
        }
    }

    private static int bfs(Point[] points, int I) {
        // BFS 탐색을 위한 큐 생성 및 시작점 추가
        Queue<Point> q = new LinkedList<>();
        q.offer(points[0]);

        // 방문 여부를 저장하는 2차원 배열
        boolean visited[][] = new boolean[I][I];
        visited[points[0].x][points[0].y] = true; // 시작 위치 방문 처리

        while (!q.isEmpty()) {
            Point poll = q.poll(); // 큐에서 현재 위치 꺼내기

            // 목표 지점에 도달하면 이동 횟수 반환
            if (poll.x == points[1].x && poll.y == points[1].y) {
                return poll.count;
            }

            // 나이트의 이동 방향(8방향) 탐색
            for (int i = 0; i < 8; i++) {
                int dirX = poll.x + dX[i];
                int dirY = poll.y + dY[i];

                // 체스판 범위를 벗어나는 경우 무시
                if(dirX < 0 || dirX >= I || dirY < 0 || dirY >= I){
                    continue;
                }

                // 방문하지 않은 위치만 큐에 추가
                if(!visited[dirX][dirY]){
                    visited[dirX][dirY] = true; // 방문 처리
                    q.offer(new Point(dirX, dirY, poll.count + 1)); // 이동 횟수 +1 후 큐에 추가
                }
            }
        }

        return -1; // 도달할 수 없는 경우 (문제에서는 항상 가능하다고 가정)
    }
}


```

## 📌 코드 설명

## 1) 입력 처리

- BufferedReader와 StringTokenizer를 사용하여 입력을 빠르게 처리합니다.
- T: 테스트 케이스 수를 입력받습니다.
- I: 체스판의 크기를 입력받습니다.
- `points[0]`: 시작 위치 저장
- `points[1]`: 목표 위치 저장

## 2) BFS 탐색

- `Queue<Point>`를 이용하여 BFS 탐색을 수행합니다.
- `visited[][]` 배열을 사용하여 중복 방문을 방지합니다.
- poll.count: 현재까지의 이동 횟수를 저장하고, 목표 지점에 도달하면 즉시 반환합니다.
- 8방향 이동(dx[], dy[])을 사용하여 나이트의 이동을 구현합니다.

## 3)🔹 BFS를 사용하는 이유

- 최단 거리 문제에서 최적의 해를 찾기 위해 **BFS (Breadth-First Search, 너비 우선 탐색)**를 사용합니다.
- BFS는 같은 레벨의 노드를 먼저 탐색하므로, 최단 경로를 보장합니다.
