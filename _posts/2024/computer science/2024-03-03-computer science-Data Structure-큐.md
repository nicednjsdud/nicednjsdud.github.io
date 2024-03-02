---
title: (알고리즘) 바킹독의 실전 알고리즘 0x06강 ( 큐 )
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 바킹독의 실전 알고리즘 0x03강 ( 스택 )
tag: BackJoon
article_tag1: BackJoon
article_section: BackJoon
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2024-03-03 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x06강 ( 큐 )

## 목차

- 0x00 정의와 성질
- 0x01 기능과 구현
- 0x02 STL list
- 0x03 연습 문제

## 1. 정의와 성질

- 큐는 한쪽 끝에서 원소를 넣고 반대쪽 끝애서 원소를 뺄 수 있는 자료구조
- 스택에서는 먼저 들어간 원소가 나중에 나왔는데, 큐에서는 먼저 들어간 원소가 먼저나오게 됨
- ex) 공항에서 입국수속을 하는 줄과 같은 상황
- **FIFO(First In First Out)**

![alt](/assets/images/post/ComputerStudy/1093.png)

### 1) 큐의 성질

1. 원소의 추가가 O(1)
2. 원소의 삭제가 O(2)
3. 제일 앞/뒤 원소 확인이 O(1)
4. 제일 앞/뒤가아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

## 2. 기능과 구현

![alt](/assets/images/post/ComputerStudy/1094.png)

```c
#include <bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[MX];
int head = 0, tail = 0

void push(int x){
 dat[tail++] = x;
}

void pop(){
 head++;
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

### 1) push 함수

![alt](/assets/images/post/ComputerStudy/1095.png)

### 2) pop 함수

![alt](/assets/images/post/ComputerStudy/1096.png)

### 3) front/back 함수

![alt](/assets/images/post/ComputerStudy/1097.png)

## 3. STL queue

```c
#include<bits/stdc++.h>
using namespace std;

int main(void){
  queue<int> Q;
  Q.push(10);     //10
  Q.push(20);     //10 20
  Q.push(30);     //10 20 30
  cout << Q.size() << '\n'; //3
  if(Q.empty()) cout << "Q is empty\n";
  else cout << "Q is not empty\n"; Q is not empty
  Q.pop();        //20 30
  cout << Q.front() << '\n' // 20
  cout << Q.back() << '\n'  // 30
  Q.push(40); // 20 30 40
  Q.pop();  // 30 40
  cout << Q.front() << '\n' // 30
}
```

## 4. 연습문제

### 1) BOJ 10845: 큐

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10845/">BackJoon Algorithm 10845 큐 (Java)</a>

## 출처

<a href="https://www.youtube.com/watch?v=D_fwSy5tRAY&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=7">[바킹독의 실전 알고리즘] 0x06강 - 큐</a>
