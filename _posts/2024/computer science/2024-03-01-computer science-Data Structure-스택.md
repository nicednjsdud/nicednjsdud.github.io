---
title: (알고리즘) 바킹독의 실전 알고리즘 0x05강 ( 스택 )
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
last_modified_at: "2024-03-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x04강 ( 스택 )

## 목차

- 0x00 정의와 성질
- 0x01 기능과 구현
- 0x02 STL list
- 0x03 연습 문제

## 1. 정의와 성질

- 한쪽 끝에서만 원소를 넣거나 뺄수 있는 자료구조
- ex) 프링글스 통, 엘리베이터
- FILO(Fisrt In Last Out) 자료 구조
- 스택, 큐,덱은 특정위치에 원소만 삽입,삭제가 가능 (Restricted Structure)

![alt](/assets/images/post/ComputerStudy/1089.png)

### 1) 스택의 성질

1. 원소의 추가가 O(1)
2. 원소의 제거가 O(1)
3. 제일 상단의 원소 확인이 O(1)
4. 제일 상단이 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

## 2. 기능과 구현

```c
#include <bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[MX];
int pos = 0;

void push(int x){
  dat[pos++] = x;
}
void pop(){
  pos--;
}

int top(){
  return dat[pos-1];
}

void test(){

}

int main(void){
  test();
}
```

1

### 1) push 함수

![alt](/assets/images/post/ComputerStudy/1090.png)

```c
void push(int x){
  dat[pos++] = x;
}
```

### 2) pop 함수

![alt](/assets/images/post/ComputerStudy/1091.png)

```c
void pop(){
  pos--;
}
```

### 3) top 함수

![alt](/assets/images/post/ComputerStudy/1092.png)

```c
int top(){
  return dat[pos-1];
}

```

## 3. STL stack

```c
#include <bits/stdc++.h>
using naemspace std;

int main(void){
  stack<int> S;
  S.push(10);     // 10
  S.push(20);     // 10 20
  S.push(30);     // 10 20 30
  cout << S.size() << '\n' // 3
  if(S.empty()) cout << "S is empty\n";
  else cout << "S is not empty\n";  // S is not empty
  S.pop(); // 10 20
  cout << S.top() << '\n'; // 20
  S.pop(); // 10
  cout << S.top() << '\n'; // 10
  S.pop(); // empty
  if(S.empty()) cout << "S is empty\n"; // s is empty
  cout << S.top() << '\n'; // runtime error 발생
}
```

## 4. 연습 문제

### 1) BOJ 10828 : 스택

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10828/">BackJoon Algorithm 10828 스택 (Java)<a>

### 2) BOJ 10773 : 재로

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10773/">BackJoon Algorithm 제로 10773 (Java)<a>

## 출처

<a href="https://www.youtube.com/watch?v=0DsyCXIN7Wg">[바킹독의 실전 알고리즘] 0x05강 - 스택</a>
