---
title: (자료구조) 5-2 단순 연결 리스트
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 단순 연결 리스트
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-25 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 단순 연결 리스트

## 1. 단순 연결 리스트의 개요

### 1) 개념

- 노드가 하나의 링크 필드에 의해서 다음 노드와 연결된 구조를 갖는 연결 리스트
- 연결 리스트, 선형 연결 리스트(Linear Linked List), 단순 연결 선형 리스트
  (Singly Linked Linear List)라고도 함.

### 2) 단순 연결 리스트의 예

- 이름표를 하나만 가지고 한쪽으로만 연결된 인간 기차

![alt](/assets/images/post/ComputerStudy/207.png)

- 단순 연결 리스트 week2

![alt](/assets/images/post/ComputerStudy/208.png)

## 2. 단순 연결 리스트의 삽입과 삭제

### 1) 삽입 연산

- 리스트 week2 = (월,금,일)에서 원소 "월","금" 사이에 "수"를 삽입

#### (1)

- 삽입할 새 노드를 만들 공백 new(150번지의 노드)를 메모리에 할당 받아서 포인터 변수 new가 가리키게함

![alt](/assets/images/post/ComputerStudy/209.png)

#### (2)

- new 노드의 데이터 필드에 "수"를 저장함

![alt](/assets/images/post/ComputerStudy/210.png)

#### (3)

- new 노드의 앞 노드 즉 "월" 노드의 링크 필드값(200)을 new 노드 링크 필드에 저장

![alt](/assets/images/post/ComputerStudy/211.png)

#### (4)

- new 노드의 값(new 노드가 가리키고 있는 새 노드의 주소 150)을 **"월" 노드의 링크 필드에 저장**

![alt](/assets/images/post/ComputerStudy/212.png)

#### (5)

- 단순 연결 리스트의 삽입 연산에서는 물리적 순서를 유지하기 위해서 원소들을 이동시키지 않고,  
  **링크 필드의 포인터값에 대한 연산만으로 삽입 연산을 수행하는 장점**

### 2) 삭제 연산

- 리스트 week2 = (월,수,금,일)에서 원소 "수"를 삭제

#### (1)

- **삭제할 노드의 앞 노드**(선행자) 찾기

![alt](/assets/images/post/ComputerStudy/213.png)

#### (2)

- 삭제할 원소의 앞 노드 **"월" 노드의 링크 필드에 삭제 노드의 링크 필드값을 저장**

![alt](/assets/images/post/ComputerStudy/214.png)

#### (3)

- 단순 연결 리스트의 삭제 연산에서도 원소들을 이동시키지 않고 **링크 필드의 포인터값에 대한 연산**  
  만으로 **삭제 연산을 수행**

## 3. 자유 공간 리스트 (Free Space List)

### 1) 정의

- 메모리를 사용하기 전에 미리 노드로 나누어서 연결해 놓은 리스트
- 새 노드가 필요할 때 리스트에서 할당 받아 사용하고, 사용하지 않는 노드는 다시 리스트로 반환
- 연산과정과 메모리 관리가 효율적으로 이루어짐

### 2) 자유 공간 리스트의 예

![alt](/assets/images/post/ComputerStudy/215.png)

![alt](/assets/images/post/ComputerStudy/216.png)

### 3) 자유 공간 리스트에서 노드 할당

#### (1) 노드 할당 알고리즘

```c
  getNode()
          if(Free = null) then
              underflow();      // 언더플로우 처리 루틴
          new  <- Free;         // (1-2)
          Free <- Free.link;    // (1-3)
          return new;
  end getNode()
```

##### (1-1) 자유 공간 리스트에서의 노드 할당 과정

- 자유 공간 리스트 free에서 노드를 할당할 때에는 항상 첫 번째 노드를 할당
- 초기상태

![alt](/assets/images/post/ComputerStudy/217.png)

##### (1-2) new <- Free;

- 리스트 Free의 첫 번째 노드의 주소(100)를 포인터 new에 저장하여 포인터 new가 할당할 노드를  
  가리키게 함

![alt](/assets/images/post/ComputerStudy/218.png)

##### (1-3) Free <- Free.link;

- 포인터 Free에 리스트의 두 번째 노드의 주소(Free.link)를 저장

![alt](/assets/images/post/ComputerStudy/219.png)

### 4) 자유 공간 리스트로의 노드 반환

#### (1) 자유 공간 리스트에서의 노드 할당 과정

- 사용이 끝난 노드를 자유 공간 리스트 Free의 첫 번째 노드로 다시 삽입
- 초기상태

![alt](/assets/images/post/ComputerStudy/220.png)

#### (2) 노드 반환 알고리즘

```c
  returnNode(old)
        old.link <- Free;     // (2-1)
        Free <- old;
  end returnNode()
```

##### (2-1) old.link <- Free;

- 자유 공간 리스트 Free의 첫 번째 노드 주소(200)를 반환할 노드 포인터 old.link에 저장
