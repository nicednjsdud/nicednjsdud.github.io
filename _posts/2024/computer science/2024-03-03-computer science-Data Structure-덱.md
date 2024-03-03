---
title: (알고리즘) 바킹독의 실전 알고리즘 0x07강 ( 덱 )
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
last_modified_at: "2024-03-03 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x07강 ( 덱 )

## 목차

- 0x00 정의와 성질
- 0x01 기능과 구현
- 0x02 STL list
- 0x03 연습 문제

## 1. 정의와 성질

- Restricted Structrue의 끝판왕과 같은 느낌의 자료구조
- 양쪽에서 삽입과 삭제가 전부 가능
- 자료구조의 덱은 deque
- Double Ended Queue

![alt](/assets/images/post/ComputerStudy/1098.png)

### 1) 덱의 성질

1. 원소의 추가가 O(1)
2. 원소의 제거가 O(1)
3. 제일 앞/뒤의 원소 확인이 O(1)
4. 제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원친적으로 불가능

## 2. 기능과 구현

```c
#include<bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[2*MX+1];
int head =MX, tail=MX;

void push_front(int x){
  dat[--head] = x;
}
void push_back(int x){
  dat[tail++] = x;
}
void pop_front(){
  head++;
}
void pop_back(){
  tail--;
}
int front(){
  return dat[head];
}
int back(){
  return dat[tail-1];
}
void test(){
  ...
}

int main(void){
  test();
}
```

## 3. STL deque

```c
#include <bits/stdc++.h>
using namespace std;

int main(void){
  deque<int> DQ:
  DQ.push_front(10);    // 10
  DQ.push_back(50);     // 10 50
  DQ.push_front(24)l    // 24 10 50
  for(auto x : DQ) cout << x;
  cout << DQ.size() << '\n';   // 3
  if(DQ.empty()) cout << "DQ is empty '\n'"; // DQ is not empty
  DQ.pop_front();       // 10 50
  DQ.pop_back();        // 10

  cout << DQ.back() << '\n'; // 10
  DQ.push_back(72);   // 10 72
  cout << DQ.front() << '\n'; // 10
  DQ.push_back(12);   // 10 72 12
  DQ[2] = 17;   // 10 72 17
  DQ.insert(DQ.begin() + 1, 33);  // 10 33 72 17
  DQ.insert(DQ.begin() + 4, 60);  // 10 33 72 17 60
  for(auto x : DQ) cout << x << ' ';
  cout << '\n';
  DQ.erase(DQ.begin() + 3); // 10 33 72 60
  cout << DQ[3] << '\n' // 60
  DQ.clear(); // DQ의 모든 원소 제거

}
```

## 4. 연습 문제

### 1) BOJ 10866번 : 덱

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10866/">BackJoon Algorithm 10866 덱 (Java)</a>

## 출처

<a href="https://www.youtube.com/watch?v=D_fwSy5tRAY&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=8">[바킹독의 실전 알고리즘] 0x07강 - 덱</a>
