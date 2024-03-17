---
title: (알고리즘) 바킹독의 실전 알고리즘 0x08강 ( 스택의 활용 )
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
last_modified_at: "2024-03-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x08강 ( 스택의 활용 )

## 목차

- 0x00 수식의 괄호 쌍이란?
- 0x01 문제 해결을 위한 관찰
- 0x02 문제 해결 방법
- 0x03 연습 문제

## 1. 수식의 괄호 쌍이란?

```
  32 - { 6 - ( 2 + 4 ) * 7}
```

- 수식의 괄호 쌍이란, 주어진 괄호 문자열이 올바른지 판단하는 문제

## 2. 문제 해결을 위한 관찰

### 1) 괄호가 한 가지일때

```
  (())()()        // O
  ))(()           // X
  ()())(()        // X
```

- 여는 괄호와 닫는 괄호 개수가 동일하다.
- 서로 쌍을 이룬다.

### 2) 괄호가 두 가지 이상

```
  ({})          // O
  ({)}          // X
```

- 여는 괄호 닫는 개수가 동일해도 올바르지가 않다.

### 3) 관찰

- 문자열을 앞에서부터 읽어나갈 때 , 닫는 괄호는 남아있는 괄호 중에서 가장 최근에  
  들어온 여는 괄호와 짝을 지어 없애버리는 명령이라고 생각해도 된다.

## 3. 문제 해결 방법

1. 여는 괄호가 나오면 스택에 추가
2. 닫는 괄호가 나왔을 경우
   1. 스택이 비어있으면 올바르지 않은 괄호 쌍
   2. 스택의 top이 짝이 맞지 않은 괄호일 경우 올바르지 않은 괄호 쌍
   3. 스택의 top이 짝이 맞는 괄호일 경우 pop
3. 모든 과정을 끝낸후 스택에 괄호가 남아있으면 올바르지 않은 괄호 쌍, 남아있지 않으면 올바른 괄호 쌍

## 4. 연습 문제

### 1) BOJ 4949번 : 균형잡인 세상

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_4949/">BackJoon Algorithm 균형잡힌 세상 4949 (Java)</a>

### 2) BOJ 10799번 : 쇠막대기

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_10799/">BackJoon Algorithm 10799 쇠막대기 (Java)</a>

### 3) BOJ 2504 : 괄호의 값

<a href=""></a>

## 출처

<a href="https://www.youtube.com/watch?v=cdjjk-ryPKc&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=9">[바킹독의 실전 알고리즘] 0x07강 - 덱</a>
