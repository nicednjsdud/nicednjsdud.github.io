---
title: (자료구조) 13-1 정렬 (버블 정렬)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 정렬 1
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-18 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 정렬 1

## 1. 버블 정렬

- 인접한 두 개의 원소를 비교하여 자리를 교환하는 방식으로 정렬

### 1) 수행 방법

- 첫 번째 원소부터 마지막 원소끼리 반복하여 한 단계가 끝나면 큰 원소가 마지막 자리로 정렬
- 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 마지막 자리로 이동하는 모습이 물 속에서 물 위로  
  물방울 모양과 같다고 하여 **버블(bubble) 정렬**이라함

### 2) 선택 정렬 수행 과정

- 정렬되지 않은 `{69,10,30,2,16,8,31,22}`의 자료들을 선택 정렬 방법으로 정렬하는 과정

#### (1)

- 인접한 두 원소를 비교하여 자리를 교환하는 작업을 첫 번째 원소부터 마지막 원소까지 차례로 반복하여 가장 큰 원소  
  `69`를 마지막 자리로 정렬

![alt](/assets/images/post/ComputerStudy/717.png)
![alt](/assets/images/post/ComputerStudy/718.png)

#### (2)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `31`을 끝에서 두 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/719.png)
![alt](/assets/images/post/ComputerStudy/720.png)

#### (3)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `30`을 끝에서 세 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/721.png)
![alt](/assets/images/post/ComputerStudy/722.png)

#### (4)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `22`를 끝에서 네 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/723.png)

#### (5)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `16`을 끝에서 다섯 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/724.png)

#### (6)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `10`을 끝에서 여섯 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/725.png)

#### (7)

- 버블 정렬을 수행하여 나머지 원소 중에서 가장 큰 원소 `8`을 끝에서 일곱 번째 자리로 정렬

![alt](/assets/images/post/ComputerStudy/726.png)

- 마지막에 남은 첫 번째 원소는 전체 원소 중에서 가장 작은 원소로 이미 정렬된 상태이므로 실행을 종료

### 3) 버블 정렬 알고리즘

```c
  bubbleSort(a[],n)
      for (i <- n - 1 ; i >= 0 ; i <- i - 1){
          for ( j <- 0 ; j < i ; j <- j + 1){

                if (a[j]>a[j+1]) then {
                    temp <- a[j];
                    a[j] <- a[j+1];
                    a[j+1] <- temp;
                }
          }
      }
  end bubbleSrot();
```

#### (1) 메모리 사용 공간

- n개의 원소에 대하여 n개의 메모리 사용

#### (2) 연산 시간

##### (2-1) 최선의 경우

- 자료가 이미 정렬되어 있는 경우
- 비교횟수 : i번째 원소를 (n-1)번 비교하므로 n(n-1)/2번
- 자리 교환 횟수 : 자리교환이 발생하지 않음

##### (2-2) 최악의 경우

- 자료가 역순으로 정렬되어 있는 경우
- 비교 횟수 : i번째 원소를 (n-1)번 비교하므로 n(n-1)/2번
- 자리 교환 횟수 : i번째 원소를 (n-1)번 비교하므로 n(n-1)/2번

##### (2-3)

- 평균 시간 복잡도는 O(n(2승))이 됨
