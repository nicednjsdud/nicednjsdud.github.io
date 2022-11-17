---
title: (시스템 프로그래밍) 4-3 타이머 관리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 사용자 관리
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-17 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 타이머 관리

## 1. 리눅스 시스템 타이머

- 1970년 1월 1일 0시 0분 0초(UTC)를 기준으로 현재까지 경과한 시간을 초 단위로 저장하고  
  이를 기준으로 시간 정보 관리

### 1) 기본 시간 정보 확인

#### (1) 초 단위로 현재 시간 정보 얻기 : time(2)

```c
  #include <sys/types.h>
  #include <time.h>

  time_t time(time_t *tloc);
```

- tloc : 검색할 시간 정보를 저장할 주소

#### (2) 마이크로 초 단위로 시간 정보얻기 : gettimeofday(3)

```c
  #include <sys/time.h>

  int gettimeofday(struct timeval *tp, void *tzp);
  int settimeofday(struct timeval *tp, void *tzp);
```

- tp : 시간 정보 구조체 주소
- tzp : 시간대

### 2) 시간대 정보 : tzset(3)

- 현재 지역의 시간대로 시간을 설정

```c
  #include <time.h>

  void tzset(void);
```

- 이 함수를 호출하면 전역변수 4개에 정보를 설정

```c
  extern time_t timezone, altzone;
  extern int daylight;
  extern char *tzname[2];
```

#### (1) timezone

- UTC와 지역 시간대와 시차를 초 단위로 저장

#### (2) altzone

- UTC와 일광절약제 등으로 보정된 지역시간대와의 시차를 초 단위로 저장

#### (3) daylight

- 일광절약제를 시행하면 0 이외의 값, 시행하지 않으면 0

#### (4) tzname

- 지역시간대와 보정된 시간대명을 약어로 저장

### 3) 시간의 형태 변환

#### (1) 초단위 시간 정보 분해 : gmtime(3), localtime(3)

```c
  #include <time.h>

  struct tm *localtime(const time_t *clock);
  struct tm *gmtime(const time_t *clock);
```

- 초를 인자로 받아 tm구조 리턴, gmtime은 UTC기준, localtime은 지역시간대 기준

#### (2) 초단위 시간으로 역산 : mktime(3)

```c
  #include <time.h>

  time_t mktime(struct tm *timeptr);
```

#### (3) tm구조체

![alt](/assets/images/post/ComputerStudy/70.png)

- tm_mon(월) : 0(1월) ~ 11 (12월)
- **tm_year(연도) : 년도 - 1900**
- tm_wday(요일) : 0(일) ~ 6(토)
- tm_isdst(일광절약제) : 1(시행)

## 2. 리눅스 시스템 타이머 함수

### 1) 형식 지정 시간 출력

#### (1) 초단위 시간을 변환해 출력하기 : ctime(3)

```c
  #include <time.h>

  char *ctime(const time_t *clock);
```

- clock : 초 단위 시간을 저장한 주소

#### (2) tm 구조체 시간을 변환해 출력하기 : asctime(3)

```c
  #include <time.h>

  char *asctime(const struct tm *tm);
```

- tm : 시간정보를 저장한 tm 구조체 주소

#### (3) 출력 형식 기호 사용 : strftime(3)

```c
  #include <time.h>

  size_t strftime(char *restrict s, size_t maxsize,
            const char *restrict format, const struct tm *restrict timeptr);
```

- s : 출력할 시간 정보를 저장할 배열 주소
- maxsize : s의 크기
- format : 출력 형식
- timeptr : 출력할 시간정보를 저장한 구조체 주소

#### (4) 형식 지정 시간 출력

![alt](/assets/images/post/ComputerStudy/71.png)
![alt](/assets/images/post/ComputerStudy/72.png)
