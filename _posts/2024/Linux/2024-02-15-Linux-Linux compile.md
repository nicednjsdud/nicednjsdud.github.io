---
title: (리눅스)2. 커널 컴파일
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Linux
description: Linux
tag: Linux
article_tag1: Linux
article_section: Linux
meta_keywords: Linux
last_modified_at: "2024-02-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 커널 컴파일

## 목차

1. CPU 밴더
2. SOC 벤더
3. 라즈베이 파이란?

## 1. CPU 밴더

1. ARM : ARMv7, ARMv8
2. 인텔 : x86
3. IBM(PowerPC)
4. AMD(Athlon)

- CPU 아키텍처를 제공하는 회사

### 1) CPU가 달라지면?

- 시스템 콜, 익셉션, 컨텍스트 스위치
- 커널의 핵심 동작은 서로 다른 CPU 어셈블리 코드로 구현되어 있음
- 컨텍스트 스위칭 세부 동작은 x86, ARMv7같은 CPU별로 구현 방식이 다름

## 2. SOC 벤더

1. 브로드컴
2. 삼성전자 : 엑스노스
3. 퀄컴 : 스탭 드래곤
4. 인텔 : 아톰, 무어필드
5. 미디어텍 : 헬리오
6. 엔비디아 : 테그라

- 하나의 칩 : CPU + 메모리 + 주변장치 + 무선통신

## 3. 보드 벤더 및 OEM

- 보드 벤더 : (라즈베리 파이)

### 1) OEM

- 삼성 전자와 같은 사용 제품 만드는 곳
- 스마트폰 만드는 곳

## 4. 라즈베리 파이란?

1. 세계적으로 쓰이는 리눅스 개발용 보드, 소형 컴퓨터
2. 가격 대비 성능이 좋음
3. 막강한 커뮤니티 : 자료가 많음
4. 저렴한 가격 : 저렴한 편인데 , 지금은 좀 비쌈
5. 간단한 설치 : 리눅스 설치가 용이
6. 다양한 이미지가 존재
7. 최신 커널 지원
