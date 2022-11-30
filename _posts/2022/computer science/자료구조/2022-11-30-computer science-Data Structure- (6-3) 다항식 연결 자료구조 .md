---
title: (자료구조) 6-3 다항식 연결 자료 구조
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 다항식 연결 자료 구조
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-30 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 다항식 연결 자료 구조

## 1. 다항식의 연결 자료 구조

### 1) 다항식의 연결 자료구조 표현

- 단순 연결 리스트를 이용하여 다항식을 표현
- 다항식의 항 : 단순 연결 리스트의 노드

#### (1) 노드 구조

![alt](/assets/images/post/ComputerStudy/302.png)

- 각 항에 대해서 계수와 지수를 저장
- 계수를 저장하는 coef와 지수를 저장하는 expo의 두개 필드로 구성
- 링크 필드는 다음항을 연결하는 포인터 구조

#### (2) 노드에 대한 구조체 정의

```c
  typedef struct Node{
    float coed;
    int expo;
    struct Node *link;
  }
```

### 2) 다항식의 단순 연결 리스트 표현

- 오른쪽 식 지수 () 표현
- 다항식 A(x) = 4x(3) + 3x(2) + 5x
- 다항식 B(x) = 3x(4) + x(3) + 2x + 1

![alt](/assets/images/post/ComputerStudy/303.png)

## 2. 다항식 연결 자료구조의 삽입 연산

### 1) 다항식 연결 자료구조의 항 삽입 연산

- 다항식에 항을 추가하는 알고리즘

* 다항식 리스트 포인터 PL과 coef 필드값을 저장한 변수 coef, expo 필드값을 저장한 변수 expo 그리고  
  리스트 PL의 마지막 노드의 위치를 지시하는 포인터 last를 변수로 사용

```c
  appendTerm(PL, coef, expo, last)
      new <- getNode();
      new.expo <- expo;
      new.coef <- coef;
      new.link <- null;
      if (PL = null) then {       // (1) 공백 리스트인 경우
          PL <- new;              // (1-1)
          last <- new;            // (1-2)
      }
      else{                       // (2) 공백 리스트가 아닌 경우
          last.link <- new;       // (2-1)
          last <- new;            // (2-2)
      }
  end appendTerm()
```

#### (1) 공백 리스트 인 경우

![alt](/assets/images/post/ComputerStudy/304.png)

##### (1-1) PL <- new;

- 포인터 new의 값을 리스트 포인터 PL에 저장하여 노드 new가 리스트 PL의 첫 번째 노드가 되도록 연결

##### (1-2) last <- new;

![alt](/assets/images/post/ComputerStudy/305.png)

#### (2) 공백 리스트가 아닌 경우

- 새노드 new를 리스트 PL의 마지막 노드로 삽입함

![alt](/assets/images/post/ComputerStudy/306.png)

##### (2-1) last.link <- new;

- 포인터 new의 값을 노드 last의 링크에 저장하여 노드 new를 노드 last의 다음 노드로 연결함

##### (2-2) last <- new;

- 포인터 new의 값을 노드 last에 저장하여 노드 new를 리스트 PL의 마지막 노드로 설정함

## 3. 다항식 연결 자료구조의 덧셈 연산

### 1) 덧셈 A(x) + B(x) = C(x)를 단순 연결 리스트 자료구조를 사용하여 연산

- 다항식 A(x)와 B(x), C(x)의 항을 지시하기 위해서 세개의 포인터를 사용
- 포인터 p : 다항식 A(x)에서 비교할 항을 지시
- 포인터 q : 다항식 B(x)에서 비교할 항을 지시
- 포인터 r : 덧셈연산 결과 만들어지는 다항식 C(x)의 항을 지시

### 2) p.expo < q.expo : 다항식 A(x)항의 지수가 작은 경우

- 두 다항식의 지수가 서로 다른 경우 계수의 덧셈을 할 수 없고 지수가 높은 항부터 나열
- 포인터 q가 가리키는 다항식 B(x)의 항을 C(x)항으로 복사
- q가 가리키는 항에 대한 처리가 끝났으므로 q를 다음 노드로 이동

![alt](/assets/images/post/ComputerStudy/307.png)

### 3) p.expo = q.expo : 두 항의 지수가 같은 경우

- p.coef와 q.coef를 더하여 C(x)의 항인 r.coef에 저장하고 지수는 같으므로 p.expo(또는 q.expo)를  
  r.expo에 저장
- 다음 항을 비교하기 위하여 p, q를 각각 다음 노드로 이동

![alt](/assets/images/post/ComputerStudy/308.png)

### 4) p.expo > q.expo : 다항식 A(x) 항의 지수가 큰 경우

- p가 가리키는 다항식 A(x)의 항의 지수가 더 큰 경우에는 포인터 p가 가리키는 항을 C(x)의 항으로 복사
- 포인터 p에 대한 처리가 끝났으므로 p를 다음 노드로 이동

![alt](/assets/images/post/ComputerStudy/309.png)
