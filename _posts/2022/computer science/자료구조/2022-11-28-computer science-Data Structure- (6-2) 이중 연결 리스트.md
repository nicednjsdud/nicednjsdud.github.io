---
title: (자료구조) 6-2 이중 연결 리스트
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 이중 연결 리스트
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 이중 연결 리스트

## 1. 이중 연결 리스트

### 1) 정의

- 원형 연결 리스트에서 현재 노드의 이전 노드를 접근하려면 전체 리스트를 한 바퀴 순회해야 하는  
  문제가 있어 이를 해소하기 위해 양쪽 방향으로 순회할 수 있도록 노드를 연결한 리스트

#### (1) 이중 연결 리스트 구조

- 두개의 링크 필드와 한 개의 데이터 필드로 구성
- llink(Left Link) 필드는 왼쪽 노드와 연결하는 포인터
- rlink(Right Link) 필드는 오른쪽 노드와 연결하는 포인터

![alt](/assets/images/post/ComputerStudy/282.png)

#### (2) 이중 연결 리스트 노드의 구조체 정의

```c
  typedef struct Dnode{
    struct Dnode *llink;
    char data[5];
    struct Dnode *rlink;
  }
```

### 2) 단방향 vs 양방향 기차

- 단방향

![alt](/assets/images/post/ComputerStudy/283.png)

- 양방향

![alt](/assets/images/post/ComputerStudy/284.png)

- 양방향 기차를 이중 연결 리스트라고 가정하면 아이들은 노드가 되고, 왼속에 있는 이름표 llink,  
  오른손에 있는 이름표는 rlink가 됨

### 3) 이중 연결 리스트 예제

#### (1) 리스트 week = (월,수,금)의 이중 연결 리스트 구성

![alt](/assets/images/post/ComputerStudy/285.png)

- 이중 연결 리스트에서 첫 번째와 마지막 노드가 아닌 임의의 노드 p에 대하여 다음이 성립
- **p = plink.rlink = prlink.llink**

#### (2) 리스트 week = (월,수,금)의 원형 이중 연결 리스트

![alt](/assets/images/post/ComputerStudy/286.png)

- 이중 연결 리스트를 원형으로 구성

## 2. 이중 연결 리스트의 삽입

### 1) 양방향 기차 놀이에서 사람 추가하기

![alt](/assets/images/post/ComputerStudy/287.png)

#### (1)

- 철이의 왼쪽 사람이 될 승희의 오른쪽 이름표를 철이의 오른손에 주고 대신 '철이' 이름표를 승희에게 줌

![alt](/assets/images/post/ComputerStudy/288.png)

#### (2)

- 철이의 오른쪽이 될 상원의 왼손 이름표를 철이의 왼손에 주고 대신 '철이' 이름표를 상원에게 줌

![alt](/assets/images/post/ComputerStudy/289.png)

#### (3)

- 이름표대로 연결하면 양방향 기차가 완성됨

![alt](/assets/images/post/ComputerStudy/290.png)

### 2) 이중 연결 리스트에서의 삽입 연산

#### (1) 이중 연결 리스트에서의 원소 삽입 연산 과정

1. 삽입할 노드를 가져옴
2. 새 노드의 데이터 필드에 값을 저장함
3. 새 노드의 왼쪽 노드의 오른쪽 링크를 새 노드의 오른쪽 링크에 저장
4. 왼쪽 노드의 오른쪽 링크에 새노드의 주소를 지정함
5. 새 노드의 오른쪽 노드의 왼쪽 링크를 새 노드의 왼쪽 링크에 저장
6. 새 노드의 왼쪽 링크에 새 노드의 주소를 저장

#### (2) 이중 연결 리스트의 원소 삽입 알고리즘

```c
  insertNode(DL, pre, x)
          new <- getNode();
          new.data <- x;
          new.rlink <- pre.rlink;   // (1)
          pre.llink <- new;         // (2)
          new.llink <- pre;         // (3)
          new.rlink.link <- new;    // (4)
  end insertNode()
```

#### 초기

- 이중 연결 리스트 DL에서 포인터 pre가 가리키는 노드의 다음 노드로 노드 new를 삽입

![alt](/assets/images/post/ComputerStudy/291.png)

#### (1) new.rlink <- pre.rlink;

- 노드 pre의 rlink를 노드 new의 rlink에 저장하여 노드 pre의 오른쪽 노드를 삽입할 노드 new의  
  오른쪽 노드로 연결

![alt](/assets/images/post/ComputerStudy/292.png)

#### (2) pre.llink <- new;

- 새 노드 new의 주소를 노드 pre의 rlink에 저장하고 노드 new를 노드 pre의 오른쪽 노드가 되도록 연결

![alt](/assets/images/post/ComputerStudy/293.png)

#### (3) new.llink <- pre;

- 포인터 pre의 값을 삽입할 노드 new의 llink에 저장하여 노드 pre를 노드 new의 왼쪽 노드가 되도록 연결

![alt](/assets/images/post/ComputerStudy/294.png)

#### (4) new.rlink.llink <- new;

- 포인터 new의 값을 노드 new의 오른쪽 노드(new.rlink)의 llink에 저장하여 노드 new의 오른쪽 노드의  
  왼쪽 노드로 노드 new를 연결

## 3. 이중 연결 리스트의 삭제

### 1) 양방향 기차 놀이에서 사람 나가기

#### (1)

- 철이의 오른손에 있는 사람의 이름표를 철이의 왼쪽에 있는 승희의 오른손에 넘겨줌

![alt](/assets/images/post/ComputerStudy/295.png)

#### (2)

- 철이의 왼손에 있는 이름표를 철이의 오른쪽에 있는 상원의 왼손에 넘겨줌

![alt](/assets/images/post/ComputerStudy/296.png)

#### (3)

- 이름표대로 연결하면 철이가 나가고 없는 양방향 기차가 됨

![alt](/assets/images/post/ComputerStudy/297.png)

### 2) 이중 연결 리스트에서의 원소 삭제 연산 과정

1. 삭제할 노드의 오른쪽 노드의 주소를 삭제할 노드의 왼쪽 노드의 오른쪽 링크에 저장함
2. 삭제할 노드의 왼쪽 노드의 주소를 삭제할 노드의 오른쪽 노드의 왼쪽 링크에 저장
3. 삭제한 노드를 자유공간 리스트에 반환

### 1) 삭제 알고리즘

```c
  deleteNode(DL, old)
        old.llink.rlink <- old.rlink;   // (1)
        old.rlink.llink <- old.llink;   // (2)
        returnNode(old);                // (3)
  end deleteNode()
```

#### 초기

- 이중 연결 리스트 CL에서 포인터 old가 가리키는 노드를 삭제하는 알고리즘

![alt](/assets/images/post/ComputerStudy/298.png)

#### (1) old.llink.rlink <- old.rlink;

- 삭제할 노드 old의 오른쪽 노드의 주소(oldrlink)를 노드 old의 왼쪽 노드의 rlink에 저장하여  
  노드 old의 오른쪽 노드를 노드 old의 왼쪽 노드의 오른쪽 노드가 되도록 연결함

![alt](/assets/images/post/ComputerStudy/299.png)

#### (2) old.rlink.llink <- old.llink;

- 삭제할 노드 old의 왼쪽 주소(llink)를 노드 old의 오른쪽 노드의 llink에 저장하여  
  노드 old의 왼쪽 노드를 노드 old의 오른쪽 노드의 왼쪽 노드가 되도록 연결함.

![alt](/assets/images/post/ComputerStudy/300.png)

#### (3) returnNode(old);

- 삭제된 노드 old를 자유 공간 리스트로 반환함

![alt](/assets/images/post/ComputerStudy/301.png)
