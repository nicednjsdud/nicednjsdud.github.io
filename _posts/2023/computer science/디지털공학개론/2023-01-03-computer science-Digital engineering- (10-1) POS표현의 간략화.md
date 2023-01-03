---
title: (디지털 공학) 10-1 POS표현의 간략화
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: POS표현의 간략화
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,디지털 공학
last_modified_at: "2023-01-03 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 디지털 공학 개론 - POS표현의 간략화

## 1. POS 표현의 간략화

- SOP형의 간략화 방법과 같지만 카르노맵에서 1이 아닌 0으로 표시된 셀을 묶어 간략화

### 1) 간략화 절차

- 카르노맵을 그린다. 여기에는 경우에 따라 아래의 두가지 방법들 중 하나가 사용될 수 있다.
- POS 부울함수를 표준형으로 변환하고, 각 항의 2진 값에 대응되는 셀에 '0'을 써넣는다.
- 혹은, 진리표에서 출력값이 '0'이되는 입력 조합에 대응되는 셀에 '0'을 넣는다.
- '0'을 가진 셀들을 2n 개 단위로 최대한 많이 포함하도록 묶음
- 각 묶음 그룹에서 비트 값이 변하는 변수는 제거하고, 변하지 않는 변수의 값이 '0' 이면 정규형  
  , '1' 이면 보수형으로 표현하여, 합의 항(term of sums)을 구함
- 합의 항들을 곱함으로써 간략화된 POS형 부울함수를 구함

### 2) 3-변수 카르노 맵을 이용한 POS표현의 간략화

```c
  F = (A+B+C')(A+B'+C')(A'+B'+C')
        001     011       111
```

![alt](/assets/images/post/ComputerStudy/533.png)

- 간략화 예 2)

```c
  F = (x+y)(x'+y+z)(x'+y+z')(x'+y'+z')
       000  100      101      111
       001
```

![alt](/assets/images/post/ComputerStudy/534.png)

- y(x'+z')

- 간략화 예 3)

```c
  F(x,y,z) = ∏(0,2,3,4,6)
```

![alt](/assets/images/post/ComputerStudy/535.png)

- (x + y')z

### 3) 4-변수 POS형 부울 함수의 간략화

```c
  F = (A+B+C+D')(A+B'+C+D')(A'+B'+C'+D')(A'+B'+C'+D)
        0001       0101      1111          1110
```

![alt](/assets/images/post/ComputerStudy/536.png)

- 답 : (A+C+D')(A'+B'+C')

- 예제 2)

```c
  F(w,x,y,z) = (w'+y+z)(w+x'+y+z)(w+x+y+z)(w+x+y'+z)(w'+x+y+z')
                1100       0100      0000    0010      1001
                1000
```

![alt](/assets/images/post/ComputerStudy/537.png)

- 답 : (y+z)(w+x+z)(w'+x+y)

## 2. POS 표현과 SOP표현간의 변환

- 하나의 카르노맵으로부터 간략화된 POS표현과 SOP표현을 모두 구할 수 있음
- 두 결과를 비교하여 더 적은 수의 게이트를 사용하는 회로를 구현

### 1) POS → SOP 변환 방법

- POS 표현에 대한 카노프 맵을 작성함
- 나머지 셀들을 '1'로 채움
- '1'의 셀들로부터 정규형 SOP 표현을 구함
- 반대 방향(SOP → POS)의 변환도 같은 방법 사용

```c
  예) F(w,x,y,z) = ∏(0,2,4,6,8,9)
    → F(w,x,y,z) = Σ(1,3,5,7,10,11,12,13,14,15)
```

![alt](/assets/images/post/ComputerStudy/538.png)

- 카르노맵으로부터 간략화한 POS 및 SOP

![alt](/assets/images/post/ComputerStudy/539.png)

- 간략화 된POS 표현 : F = (w+z)(w'+x+y)
- 간략화 된SOP 표현 : F = w'z + wx + wy

### (2) POS표현을 구하는 다른 방법

- 카노프 맵의 '0'들의 묶음 그룹으로부터 F'에 대한 SOP 표현을 구함
- (F')'을 구함으로써, F에 대한 POS 표현을 구함
- 카노프 맵으로부터 F'을 구한 후, 보수를 취하여 F를 구함

![alt](/assets/images/post/ComputerStudy/540.png)

```c
  F' = w'z'+wx'y'
  F = (F')' = (w'z'+wx'y')'
    = (w'z')'(wx'y')'
    = (w+z)(w'+x+y)
```
