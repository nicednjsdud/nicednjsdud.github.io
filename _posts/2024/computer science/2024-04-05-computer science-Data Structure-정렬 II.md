---
title: (알고리즘) 바킹독의 실전 알고리즘 0x0F강 ( 정렬 II )
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
last_modified_at: "2024-04-05 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x0F강 ( 정렬 II )

## 목차

- 0x00 Counting Sort
- 0x01 Radix Sort
- 0x02 STL sort
- 0x03 정렬의 응용

## 1. Counting Sort

![alt](/assets/images/post/ComputerStudy/1123.png)

- 위그림의 수열을 오름차순으로 정렬하고 싶다면 어떻게 할 것인가?

![alt](/assets/images/post/ComputerStudy/1124.png)

- 1은 2번, 2는 2번, 3은 2번, 4는 2번, 5는 1번 나왔다는 것을 의미

### 1) BOJ 15688번 : 수 정렬하기 5

#### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int freq[2000001];
int main(){
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  int n;
  cin >> n;

  for(int i =0; i< n ; i++){
    int a;
    cin >> a;
    freq[a+ 1000000]++;
  }
  for(int i = 0; i<= 2000000; i++){
    while(freq[i]--){
      cout << i - 1000000 << '\n';
    }
  }
}
```

#### 1-2) Java

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_15688 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
       int arr[] = new int[N];
        for(int i = 0; i < N; i++){
            arr[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(arr);

        for(int i = 0; i < N; i++){
            sb.append(arr[i]).append("\n");
        }
        System.out.println(sb);
        br.close();
    }
}

```

## 2. Radix Sort

- 자릿수를 이용해서 정렬하는 알고리즘 ( 카운팅 소트 응용 알고리즘 )

![alt](/assets/images/post/ComputerStudy/1125.png)

- 먼저 수를 하나씩 읽으면서 1의 자리에 따라 수를 넣어줌
- 리스트에 수를 다 넣은 후에는 0번 리스트부터 보면서 수를 꺼내서 재배열
- 1의자리가 같은 수는 맨 처음의 순서가 그대로 유지

![alt](/assets/images/post/ComputerStudy/1126.png)

- 정렬한 리스트에서 다시 수를 꺼내서 10의 자리에 따라 수를 넣어줌

![alt](/assets/images/post/ComputerStudy/1127.png)

- 정렬한 리스트에서 다시 수를 꺼내서 100의 자리에 따라 수를 넣어줌

### 1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n = 15;
int arr[1000001] = {...};
int d = 3;
int p10[3];

int digitNum(int x, int a){
  return ( x / p10[a]) % 10;
}

vector<int> l[10];

int main(){
  ios::sync_with_stdio(0);
  cin.tie(0);

  p10[0] = 1;
  for(int i = 1; i < d; i++) p10[i] = p10[i-1] * 10;
  for(int i = 0; i < d; i++){
    for(int j = 0; j < 10; j++) l[j].clear();
    for(int j = 0; j < n; j++)
      l[digitNum(arr[j], i)].push_back(arr[j]);
    int aidx = 0;
    for(int j = 0; j< 10; j++){
      for(auto x : l[j]) arr[aidx++] = x;
    }
  }
  for(int i = 0; i< n;i++) cout << arr[i] << ' ';
}
```

### 2) Comparision Sort, Non-comparison Sort

- 머지, 퀵, 버블 소트는 원소들끼리 크기를 비교하는 과정이 있음 (Comparison Sort)
- 카운팅, 라딕스 소트는 원소들간의 크기를 비교하지 않고 정렬을 수행 (Non-comparison Sort)

## 3. STL sort

```c
int a[5] = {1, 4, 5, 2, 7};
sort(a, a+5);

vector<int> b = {1, 4, 5, 2, 7};
sort(b.begin(), b.end());
```

## 4. 정렬의 응용

### 1) BOJ 11652 카드

#### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n;
long long a[100005];

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n;
  for(int i = 0; i<n; i++){
    cin >> a[o];
  }
  sort(a, a+n);

  int cont = 0;
  long long mxval = -(1ll << 62) - 1;
  int mxcnt = 0;

  for(int i = 0 ; i < n; i++){
    if(i == 0 || a[i-1] == a[i]) cnt++;
    else{
      if(cnt > mxcnt){
        mxcnt = cnt;
        mxval = a[i-1];
      }
      cnt = 1;
    }
  }
  if(cnt > mxcnt) mxval = a[n-1];
  cout << mxval;
}
```

#### 1-2) Java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_11652/">BackJoon Algorithm 11652 카드 (Java)
</a>

## 출처

<a href="https://www.youtube.com/watch?v=dq5t1woLJMw&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=16">[바킹독의 실전 알고리즘] 0x0F강 - 정렬 II</a>

##

7795번 풀어보기 (이분탐색 x)
