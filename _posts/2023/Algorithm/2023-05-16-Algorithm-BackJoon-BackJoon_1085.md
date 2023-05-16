---
published: true
title: BackJoon Algorithm 1018 체스판 다시 칠하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-05-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제
-
![alt](/assets/images/post/Algorithm/1018.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1018 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int row = Integer.parseInt(st.nextToken());
        int col = Integer.parseInt(st.nextToken());

        String board[] = new String[row];

        for (int i = 0; i < row; i++) {
            board[i] = br.readLine();
        }

        int sol = Integer.MAX_VALUE;

        for (int i = 0; i <= row - 8; i++) {
            for (int j = 0; j <= col - 8; j++) {
                int curSol = solved(i, j, board);

                sol = Math.min(curSol, sol);
            }
        }
        System.out.println(sol);
        br.close();
    }

    private static int solved(int startRow, int startCol, String[] board) {
        String orgBoard[] = {"WBWBWBWB", "BWBWBWBW"};
        int count = 0;

        for (int i = 0; i < 8; i++) {
            int row = startRow + i;
            for (int j = 0; j < 8; j++) {
                int col = startCol + j;

                if (board[row].charAt(col) != orgBoard[row % 2].charAt(j)) {
                    count++;
                }
            }
        }
        return Math.min(count, 64 - count);
    }
}



```
