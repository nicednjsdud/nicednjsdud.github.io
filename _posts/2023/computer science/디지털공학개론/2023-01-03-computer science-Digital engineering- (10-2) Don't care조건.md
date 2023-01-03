---
title: (디지털 공학) 10-2 Don't care 조건
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: Don't care 조건
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,디지털 공학
last_modified_at: "2022-12-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 디지털 공학 개론 - Don't care 조건

## 1. Don't care 조건

- 사용되지 않는 입력변수 조합
- 디지털 시스템에서 사용되지 않는 일부의 입력조합
- 만약 입력되는 경우 출력을 예측할 수 없는 입력
- 금지된 입력조합이 존재하는 시스템을 위한 회로를 설계할 경우 간략화를 극대화하기 위해 활용
- 예) BCD코드를 입력받아 다른 코드(예: 그레이코드)로 변환하는 회로를 구성하는 경우
  - BCD 코드 : 4비트를 필요로 하나 0~9까지만 사용
  - BCD 코드 : 0000 ~ 1001까지만 사용
  - 사용되지 않는 비트 조합들 : 1010, 1011, 1100, 1101, 1110, 1111

### 1) Don't care 조건을 사용한 회로 설계

- 사용하지 않는 비트조합의 입력이 들어오면 입력오류로 처리해야 하므로 기본적으로 그러한 입력은 들어오지 않을 것임
- 조합회로 설계 시 회로가 사용되지 않는 비트조합에 대해서는 0이나 1중에 어떤 값이 발생하던지 상관없이 회로를  
  설계할 수 있음
- 이러한 Don't care조건을 이용하여 조합회로를 단순화 시킬 수 있음

## 2. Don't care 조건을 가진 부울함수의 간략화

### 1) 간략화 절차

1. 카노프 맵에서 Don't care에 해당하는 셀을 X로 표시
2. X는 어떤 값으로든('1' 혹은 '0') 사용 가능 → 간략화에 도움이 되도록 선택하여 사용

![alt](/assets/images/post/ComputerStudy/541.png)

- 사용하지 않는 (Don't care조건) 셀 : 1010, 1011, 1100, 1101, 1110, 1111

```
   Don’t care 조건을 사용 않는 경우  F = A′BC′ + A′CD′
   Don’t care 조건을 사용 하는 경우  F = BC′ + CD′
```

#### (1) 예

```c
  예) F(w,x,y,z) = ∑(6,8,9)
    d(w,x,y,z) = ∑(10,11,12,13,14,15) : don't care 셀들
```

![alt](/assets/images/post/ComputerStudy/542.png)

```
   Don’t care 조건을 사용 않는 경우  F = (wx'y)+(w'xyz')
   Don’t care 조건을 사용 하는 경우  F = w+(xyz')
```

#### (2) 예

```
예) F(w,x,y,z) = ∏(3,4,5,6,7,12,13)
   d(w,x,y,z) = ∏(8,10,11,14,15)
```

![alt](/assets/images/post/ComputerStudy/543.png)

```
   Don’t care 조건을 사용 않는 경우  F = (w'+y)(w+x')(w+y'+z')
   Don’t care 조건을 사용 하는 경우  F = x'(y'+z')
```

#### (3) 예

```c
  예) F(x,y,z) = ∏(0,3,5,6)
     d(x,y,z) = ∏(2,7)
```

![alt](/assets/images/post/ComputerStudy/544.png)

```
   Don’t care 조건을 사용 않는 경우  F = (x+y+z)(x+y'+z')(x'+y+z')(x'+y'+z)
   Don’t care 조건을 사용 하는 경우  F = x'(y'+z')
```

#### (4) 예

```c
  예) F(x,y,z) = ∏(0,3,5,6)
     d(x,y,z) = ∏(2,7)
```

![alt](/assets/images/post/ComputerStudy/545.png)

```
   Don’t care 조건을 사용 않는 경우  간략화 X
   Don’t care 조건을 사용 하는 경우  F = y'(x'+z')(w+z)
```
