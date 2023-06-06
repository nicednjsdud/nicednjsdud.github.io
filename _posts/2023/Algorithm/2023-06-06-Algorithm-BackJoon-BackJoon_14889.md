---
published: true
title: BackJoon Algorithm 스타트와 링크 14889 (Java)
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
last_modified_at: "2023-06-06 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/14889_1.png)
![alt](/assets/images/post/Algorithm/14889_2.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Map;
import java.util.StringTokenizer;

public class Back_14889 {

    static int N;
    static int[][] arr;
    static boolean[] teamCheck;

    static int min = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        arr = new int[N][N];
        teamCheck = new boolean[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dfs(0, 0);
        System.out.println(min);
        br.close();
    }

    private static void dfs(int idx, int depth) {

        if (depth == N / 2) {

            int teamStartCount = 0;
            int teamLinkCount = 0;

            for (int i = 0; i < N - 1; i++) {
                for (int j = i + 1; j < N; j++) {
                    if (teamCheck[i] == true && teamCheck[j] == true) {
                        teamStartCount += arr[i][j];
                        teamStartCount += arr[j][i];
                    } else if (teamCheck[i] == false && teamCheck[j] == false) {
                        teamLinkCount += arr[i][j];
                        teamLinkCount += arr[j][i];
                    }
                }
            }
            int val = Math.abs(teamStartCount - teamLinkCount);

            if (val == 0) {
                System.out.println(val);
                System.exit(0);
            } else {
                min = Math.min(val, min);
            }

            return;
        }

        for (int i = idx; i < N; i++) {

            if (!teamCheck[i]) {
                teamCheck[i] = true;
                dfs(i + 1, depth + 1);
                teamCheck[i] = false;
            }
        }
    }
}


```
