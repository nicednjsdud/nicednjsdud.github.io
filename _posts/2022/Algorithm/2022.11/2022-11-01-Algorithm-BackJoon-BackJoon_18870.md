---
published: true
title: BackJoon Algorithm 좌표 압축 18870 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 좌표 압축
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-01 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/18870.png)

## 풀이

- 위에 // 두가지도 Array 배열을 정렬하는 식이다.
- 하지만 시간복잡도 문제로 시간초과가 나온다.

* **hashset을 이용하여 중복을 제거한다.**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Back_18870 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int X[] = new int[N];
        int X_location[] = new int[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        // when
        for (int i = 0; i < N; i++) {
            X[i] = Integer.parseInt(st.nextToken());
            X_location[i] = X[i];
        }
        // X_location 중복제거
        // 시간초과
//        HashSet<Integer> hashSet = new HashSet<>(Arrays.asList(X_location));
//        X_location = hashSet.toArray(new Integer[0]);
//        Arrays.sort(X_location);

        // 시간초과
//        X_location = Arrays.stream(X_location).distinct().toArray();

        Arrays.sort(X_location);

        // 중복제거
        Map<Integer, Integer> map = new HashMap<>();
        int idx = 0;
        for (int i : X_location) {
            if (!map.containsKey(i)) {
                map.put(i, idx++);
            }
        }
        // then
        for (int x : X) {
            sb.append(map.get(x)).append(" ");
        }
        System.out.println(sb);
        br.close();
    }
}



```
