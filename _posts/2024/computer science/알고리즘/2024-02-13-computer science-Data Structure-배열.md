---
title: (알고리즘) 바킹독의 실전 알고리즘 0x03강 ( 배열 )
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 바킹독의 실전 알고리즘 0x03강 ( 배열 )
tag: BackJoon
article_tag1: BackJoon
article_section: BackJoon
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2024-02-13 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x03강 ( 배열 )

## 목차

- 0x00 정의와 성질
- 0x01 기능과 구현
- 0x02 STL vector
- 0x03 연습 문제

## 배열의 성질

1. O(1)에 k번째 원소를 확인/변경 가능
2. 추가적으로 소모되는 메모리의 양`(=overhead)`가 거의 없음
3. Cache hit rate가 높음
4. 메모리 상에 연속한 구간을 잡아야 해서 할당에 제약이 걸림

## 기능과 구현

### 1) 임의의 위치에 있는 원소를 확인/ 변경 , O(1)

![alt](/assets/images/post/ComputerStudy/1075.png)

- 임의의 위치에 있는 원소를 확인, 변경 하는 연산 - O(1)
- 원소를 끝에 추가하는 연산 - O(1)
- 마지막 원소를 제거하는 것도 길이를 1줄이면 되니깐 - O(1)

### 2) 임의의 위치에 원소를 추가 , O(N)

![alt](/assets/images/post/ComputerStudy/1076.png)

- 위 사진 처럼 5번에 15를 추가했는데, 이렇게 되면 그뒤의 원소들을 전부 한 칸씩 밀어야 해서 `O(N)`이 필요

### 3) 임의의 위치에 있는 원소를 제거 , O(N)

![alt](/assets/images/post/ComputerStudy/1077.png)

- 위 사진 처럼 2번 원솔르 지웠다고 치면 그 이후에 있던 모든 원소들을 한 칸씩 땡겨와야해서 `O(N)`이 필요
- 2번 원소만 비워두면 안된냐고 생각할 수 있지만
  1. 더 이상 메모리상에 원소가 연속해서 존재하지 않기 때문에
  2. 배열의 정의에도 위배되고 또 K번째 원소를 O(1)에서 찾을 수가 없게 된다.

### 코드

```c
void insert(int idx, int num, int arr[], int& len);

void erase(int idx, int arr[], int& len);

int main(void){
  int arr[10] = {10,50,40,30,70,20};
  int len = 6;
  insert(3, 60, arr, len);  // 10 50 40 60 30 70 20
  erase(4, arr, len); // 10 50 40 60 70 20
}

```

#### 1) 구현 - insert 함수

```c
void insert(int idx, int num, int arr[], int& len){
  for(int i = len; i > idx; i--)
      arr[i] = arr[i-1];
  arr[idx] = num;
  len ++;
}

```

#### 2) 구현 - erase 함수

```c
void erase(int idx, int arr[], int& len){
  len --;
  for(int i = idx; i<len; i++)
      arr[i] = arr[i+1];
}

```

## STL vector

- vector는 배열과 거의 동일한 기능을 수행하는 자료구조
- 원소가 메모리에 연속하게 저장되어 있기 때문에 **O(1)**에 인덱스를 가지고 각 원소로 접근
- `vector는 배열과 달리 크기를 자유자재로 늘이거나 줄일 수 있다는 장점이 있음`

### 코드

```c
#include <bots/stdc++.h>
using namespace std;

int main(void){
  vector<int> v1(3, 5);       // {5,5,5}
  cout << v1.size() << '\n';  // 3
  v1.push_back(7);            // {5,5,5,7}

  vector<int> v2(2);            // {0,0}
  v2.insert(v2.begin() + 1, 3); // {0,3,0}

  vector<int> v3 = {1,2,3,4};   // {1,2,3,4}
  v3.erase(v3.begin() + 2);     // {1,2,4}

  vector<int> v4; // {}
  v4 = v3;        // {1,2,4}
  cout << v4[0] << v4[1] << v4[2] << '\n'; // 124
  v4.pop_back();  // {1,2}
  v4.clear();     // {}
}

```

- insert, earse는 시간복잡도가 **O(N)**
- push_back, pop_back은 제일 끝에 원소를 추가하거나 빼는 것이니 **O(1)**
- push_front, pop_front는 제일 앞에 원소를 추가하거나 빼는 것이니 **O(N)**

## 연습 문제

### 1) BOJ 10808번 : 알파벳 갯수

#### Java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10808/">
BackJoon Algorithm 10808 알파벳 개수 (Java)
</a>

### 2) 연습 문제

```
주어진 길이 N의 int 배열 arr에서 합이 100인 서로 다른 위치의 두원소가 존재하면
1을, 존재하지 않으면 0을 반환하는 함수 func2(int arr[], int N)을 작성하라.
arr의 각 수는 0이상 100 이하이고 N은 1000이하이다.
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_array_test {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());
        int arr[] = new int[N];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        System.out.println(func2(arr, N));
    }

     private static int func2(int[] arr, int n) {
        int occur[] = new int[101];
        for (int i = 0; i < n; i++) {
            if(occur[100-arr[i]] == 1) return 1;
            occur[arr[i]] = 1;
        }
        return 0;
    }
}


```

## 출처

<a href="https://www.youtube.com/watch?v=mBeyFsHqzHg">[바킹독의 실전 알고리즘] 0x03강 - 배열</a>
