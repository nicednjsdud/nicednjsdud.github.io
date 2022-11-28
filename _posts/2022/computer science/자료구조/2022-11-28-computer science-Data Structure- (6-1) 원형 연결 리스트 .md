---
title: (자료구조) 6-1 원형 연결 리스트
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 원형 연결 리스트
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 원형 연결 리스트

## 1. 원형 연결 리스트

### 1) 정의

- 단순 연결 리스트에서 마지막 노드가 리스트의 첫 번째 노드를 가리키게 하여 리스트의 구조를 원형으로 만든  
  연결 리스트
- 단순 연결 리스트의 마지막 노드의 링크 필드에 첫 번째 노드의 주소를 저장하여 구성
- 링크를 따라 계속 순회하면 이전 노드에 접근 가능

![alt](/assets/images/post/ComputerStudy/263.png)

### 2) 선형 vs 원형 기차놀이

- 뽑은 이름표대로 기차 연결하기

![alt](/assets/images/post/ComputerStudy/264.png)

- 선형 기차놀이 노드 표현

![alt](/assets/images/post/ComputerStudy/265.png)

- 원형 기차놀이 노드 표현

![alt](/assets/images/post/ComputerStudy/266.png)

## 2. 원형 연결 리스트의 삽입

### 1) 원형 연결 리스트의 삽입 연산

- 마지막 노드의 링크를 첫 번째 노드로 연결하는 것만 제외하고는 단순 연결 리스트의 삽입 연산과 동일

### 2) 첫 번째 노드로 삽입하기

- 원형 연결 리스트 CL에 x값을 갖는 노드 new를 삽입하는 알고리즘

```c
  insertFirstNode(CL, x)
      new <- getNode();
      new.data <- x;
      if(CL = null)then{    // (1) 공백리스트인 경우
          CL <- new;        // (1-1)
          new.link <- new;  // (1-2)
      }
      else{                 // (2) 공백리스트가 아닌 경우
          temp <- CL;       // (2-1)
          while(temp.link != CL) do // (2-2)
                temp <- temp.link;
          new.link <- temp.link;    // (2-3)
          temp.link <- new;         // (2-4)
          CL <- new;                // (2-5)
      }
```

#### (1) 원형 리스트가 공백 리스트인 경우

##### (1-1) new.data <- x;

- 삽입 하는 노드 new가 리스트의 첫 번째 노드이자 마지막 노드

![alt](/assets/images/post/ComputerStudy/267.png)

##### (1-2) new.link <- new;

- 새노드의 주소를 링크 필드에 저장하여 노드 new의 링크가 자기 자신을 가리키도록 함으로서  
  원형 연결 리스트 CL의 첫 번째 노드이자 마지막 노드가 되도록 저장함

![alt](/assets/images/post/ComputerStudy/268.png)

#### (2) 원형 리스트가 공백 리스트가 아닌 경우

##### (2-1) temp <- CL;

- 리스트가 공백이 아닌 경우 첫 번째 노드의 주소를 임시 순회 포인터 temp에 저장하여 노드 순회의 시작점을 지정

![alt](/assets/images/post/ComputerStudy/269.png)

##### (2-2) while (temp.link != CL) do temp <- temp.link;

- while 반복문을 수행하여 순회 포인터 temp 링크를 따라 **마지막 노드까지 이동**

![alt](/assets/images/post/ComputerStudy/270.png)

##### (2-3) new.link <- temp.link;

- 리스트의 **마지막 노드의 링크 값을 노드 new의 링크에 저장**하여 **노드 new가 노드 temp의 다음노드를 가리키게함**
- 리스트 CL이 원형 연결리스트이므로 마지막 노드의 다음 노드는 리스트의 첫번째 노드가 됨

![alt](/assets/images/post/ComputerStudy/271.png)

##### (2-4) temp.link <- new;

- 노드 new의 값을 포인터 temp가 가리키고 있는 마지막 노드의 링크에 저장하여 리스트에 마지막 노드가  
  노드 new로 연결되도록 함

![alt](/assets/images/post/ComputerStudy/272.png)

##### (2-5) CL <- new;

- 포인터 new의 값을 리스트 시작 포인터 CL에 설정하여 노드 new가 리스트의 첫 번째 노드가 되도록 지정함

![alt](/assets/images/post/ComputerStudy/273.png)

#### (3) 알고리즘 수행결과

- **삽입한 노드 new**는 리스트 포인터 CL과 첫 번째 노드 사이에 삽입되면서 리스트의 **새로운 첫 번째 노드가**
  되었고, **리스트의 마지막 노드와 연결하여 원형 연결 리스트 상태를 유지함**

![alt](/assets/images/post/ComputerStudy/274.png)

### 3) 중간 노드로 삽입하기

- 원형 연결 리스트 CL에 x값을 가진 노드 new를 포인터 pre가 가리키는 노드의 다음 노드로 삽입하는 알고리즘

```c
  insertMiddleNode(CL, pre, x)
          new <- getNode();
          new.data <- x;
          if(CL=null)then{      // (1) 공백리스트인 경우
              CL <- new;
              new.link <- new;
          }
          else{                 // (2) 공백리스트가 아닌경우
              new.link <- pre.link; // (2-1)
              pre.link <- new;      // (2-2)
          }
```

#### (1) 원형 리스트가 공백 리스트인 경우

- 원형 연결 리스트의 첫 번째 노드 삽입 알고리즘에서 공백 리스트에 첫 번째 노드를 삽입하는 경우와 동일

#### (2) 원형 리스트가 공백 리스트가 아닌 경우

![alt](/assets/images/post/ComputerStudy/275.png)

##### (2-1) new.link <- pre.link;

- 노드 pre의 다음 노드로 new를 삽입하기 위해서 먼저 **노드 pre의 다음노드 (pre.link)**를  
  **노드 new의 링크 필드(new.link)에 연결**함.

![alt](/assets/images/post/ComputerStudy/276.png)

##### (2-2) pre.link <- new;

- 노드 new의 값(삽입할 노드 주소)을 노드 pre의 링크 필드에 저장하여 노드 pre가  
  노드 new를 가리키도록 함

![alt](/assets/images/post/ComputerStudy/277.png)

## 3. 원형 연결 리스트의 삭제

### 1) 원형 연결 리스트에 삭제 연산

- 원형 연결 리스트 CL에서 포인터 pre가 가리키는 노드의 다음 노드를 삭제하고 삭제한 노드는 자유 공간  
  리스트로 반환
- 포인터 old는 삭제할 노드를 지시함

```c
  deleteNode(CL, Pre)
    if(CL = null) then error;
    else{
      old <- pre.link;      // (1)
      pre.link <- old.link; // (2)
      if(old = CL) then     // (3)
          CL <- old.link;   // (3-1)
      returnNode(old);      // (4)
    }
```

#### (1) old <- pre.link;

- 노드 pre의 다음 노드(pre.link)를 삭제할 노드 old로 지정함

![alt](/assets/images/post/ComputerStudy/278.png)

#### (2) pre.link <- old.link;

- 삭제할 노드 old의 다음 노드(old.link)를 노드 pre의 다음 노드(pre.link)로 지정

![alt](/assets/images/post/ComputerStudy/279.png)

#### (3) 삭제할 노드 old가 원형 연결 리스트의 첫 번째 노드인 경우

![alt](/assets/images/post/ComputerStudy/280.png)

##### (3-1) CL <- old.link;

![alt](/assets/images/post/ComputerStudy/281.png)

#### (4) returnNode(old);

- 삭제한 노드 old를 자유 공간 리스트에 반환
