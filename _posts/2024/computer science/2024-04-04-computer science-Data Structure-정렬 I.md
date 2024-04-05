---
title: (알고리즘) 바킹독의 실전 알고리즘 0x0E강 ( 정렬 I )
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 바킹독의 실전 알고리즘
tag: BackJoon
article_tag1: BackJoon
article_section: BackJoon
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2024-04-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x0E강 ( 정렬 I )

## 목차

- 0x00 기초 정렬
- 0x01 Merge Sort
- 0x02 Quick Sort

## 1. 기초 정렬

![alt](/assets/images/post/ComputerStudy/1118.png)

```c
int arr[10] = {3, 2, 7, 116, 62, 235, 1, 23, 55, 77};
int n = 10;
for(int i = n-1; i > 0; i--){
  int mxidx = 0;
  for(int j = 1; j <= i; j++){
    if(arr[mxidx] < arr[j]) mxidx = j;
  }
  swap(arr[mxidx], arr[i]);
}
```

```c
int arr[10] = {3, 2, 7, 116, 62, 235, 1, 23, 55, 77};
int n = 10;
for(int i = n-1; i > 0; i--){
  swap(*max_element(arr, arr+i+1), arr[i]);
}
```

## 2. Merge sort

- 재귀적으로 수열을 나눠 정렬한 후 합치는 정렬법
- O(NlgN)
- 먼저 길이가 N,M인 두 정렬된 리스트를 합쳐서 길이 N + M의 정렬된 리스트를 만드는 방법을 알아야 함

![alt](/assets/images/post/ComputerStudy/1119.png)

### 1) BOJ 11728번 : 배열 합치기

#### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n,m;
int a[1000005], b[1000005], c[2000005];

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  for(int i = 0; i< n; i++) cin >> a[i];
  for(int i = 0; i< m; i++) cin >> b[i];

  int aidx = 0; bidx = 0;
  for(int i = 0; i < n + m; i++){
    if(bidx == m) c[i] = a[aidx++];
    else if(aidx == n) c[i] = b[bidx++];
    else if(a[aidx] <= b[bidx]) c[i] = a[aidx++];
    else c[i] = b[bidx++];
  }
  for(int i = 0; i< n+m; i++) cout << c[i] << ' ';
}
```

#### 1-2) Java

- 풀 예정

### 2) Stable Sort

![alt](/assets/images/post/ComputerStudy/1120.png)

- 먼저 그림의 사람들을 나이순으로 정렬하는 상황
- 나머지 3명의 나이가 같이때문에 3명에 대해서 정렬이 제각각일 수 있음
- 같은 원소들끼리는 원래의 순서로 따라가도록 하는 정렬이 Stable Sort
- 정렬전 나이가 같은 사람의 옷색깔은 파랑 빨강 초록 순이니 정렬 후에도 파랑 빨강 초록 순

## 3. Quick Sort

- 퀵 소트는 머지 소트처럼 재귀적으로 구현되는 정렬
- 매 단계마다 pivot이라는 이름 붙은 원소 하나를 제자리로 보내는 작업을 반복

```c
int arr[8] = {6, -8, 1, 12, 8, 3, 7, -7};
int pivot = arr[0];
int l = 1, r= 7;
while(1){
    while(l <= r && arr[l] <= pivot) l++;
    while(l <= r && arr[r] > pivot) r00;
    if(l > r) break;
    swap(arr[l], arr[r]);
}
swap(arr[0], arr[r]);
```

### 1) 장점

- 추가적인 공간이 필요하지 않다는 점에 있다.
- 그 배열안에서 자리 바꿈만으로 처리가 되기 때문에 cache hit rate가 높아서 속도가 빠르다.

### 2) Quick sort 구현

```c
#include <bits/stdc++.h>
using namespace std;

int n = 10;
int arr[1000001] = {...};

void quick_sort(int start, int end){
    if(end <= start +1) return;
    int pivot = arr[start];
    int l = start + 1;
    int r = end -1;
    while(1){
      while(l <= r && arr[l] <= pivot) l++;
      while(l <= r && arr[r] > pivot) r00;
      if(l > r) break;
      swap(arr[l], arr[r]);
    }
  swap(arr[0], arr[r]);
  quick_sort(start, r);
  quick_sort(r+1, end);

}

int main(){
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  quick_sort(0, n);
  for(int i = 0; i< n; i++) cout << arr[i] << ' ';
}
```

### 3)

![alt](/assets/images/post/ComputerStudy/1121.png)

## 4. Merge Sort vs Quick Sort

![alt](/assets/images/post/ComputerStudy/1122.png)

## 출처

<a href="https://www.youtube.com/watch?v=59fZkZO0Bo4&t=620s">[바킹독의 실전 알고리즘] 0x0E강 - 정렬 I</a>
