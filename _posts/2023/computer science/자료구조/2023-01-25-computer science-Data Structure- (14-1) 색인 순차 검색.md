---
title: (자료구조) 14-1 색인 순차 검색
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 정렬 2
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-25 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 색인 순차 검색

## 1. 색인 순차 검색

### 1) 정의

- 정렬되어있는 자료에 대한 인덱스 테이블을 추가로 사용하여 탐색 효율을 높인 검색 방법

#### (1) 인덱스 테이블

- 배열에 정렬되어있는 자료 중에서 일정한 간격으로 떨어져있는 원소들을 저장한 테이블
- 자료에 저장되어있는 배열의 크기가 `n`이고 인덱스 테이블의 크기가 `m`일때,
- 배열에서 `n/m`간격으로 떨어져있는 원소와 그의 인덱스를 인덱스 테이블에 저장

#### (2) 검색 방법

```c
  indexTable[i].key <= key < indexTable[i+1].key
```

- 만족하는 i를 찾아서 배열의 어느 범위에 있는지를 먼저 알아낸 후에 해당 범위에 대해서만 순차 검색 수행

#### (3) 예제

![alt](/assets/images/post/ComputerStudy/788.png)

- 크기가 3인 인덱스 테이블 작성
- 인덱스 테이블에서 먼저 탐색키를 검색하여 검색 범위를 확인
- 해당 범위에 대해서만 순차 검색 실행

![alt](/assets/images/post/ComputerStudy/789.png)

#### (4) 색인 순차 검색의 성능

##### (4-1) 인덱스 테이블의 크기에 따라 결정

- 인덱스 테이블의 크기가 줄어들면 배열의 인덱스를 저장하는 간격이 커지므로 배열에서 검색해야 하는 범위도 커짐
- 인덱스 테이블의 크기를 늘리면 배열의 인덱스를 저장하는 간격이 작아지므로 배열에서 검색해야 하는 범위는  
  작아지겠지만 인덱스 테이블을 검색하는 시간이 늘어나게 됨

##### (4-2) 색인 순차 검색의 시간 복잡도

- **O(m + n/m)**
- 배열의 크기 : `n`, 인덱스 테이블의 크기 : `m`
