---
title: (시스템 프로그래밍) 3-1 리눅스 파일 특징
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 리눅스 파일 특징
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-14 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 리눅스 파일 특징

## 1. 리눅스 파일 개요 및 종류

### 1) 파일 (File)

- 관련 있는 데이터의 집합
- 정보를 저장하기 위한 가장 기본적인 단위
- 보조기억장치에 저장 ex)하드디스크, 플래쉬 메모리

### 2) 파일을 사용하는 이유

![alt](/assets/images/post/ComputerStudy/21.png)

### 3) 파일 종류

- 일반 파일 : 텍스트/ 바이너리 형태의 데이터를 저장하는 파일
- 특수 파일 : 데이터 전송장치 접근에 사용하는 파일 (device file)
- 디렉터리 : 파일 저장 위치, 공간

## 2. 리눅스 디렉토리

- 계층적
- abc 폴더에서 작업을 주로함.

![alt](/assets/images/post/ComputerStudy/22.png)

## 2. 리눅스 파일 구성 요소

### 1) 파일 구성

#### (1) file name

- 파일 접근시 사용
- 파일명과 관련된 i-node가 반드시 필요
- 최대 255자까지 가능

#### (2) i-node

- 번호로 표시
- i-node : 파일 정보 + 데이터 블록 주소
- 파일의 정보 : 파일 소유자, 파일의 크기, 접근 권한
- 데이터 블록의 실제 위치 주소

#### (3) data block

- 데이터가 저장되는 실제 하드 디스크 공간

### 2) 파일 구성 요소

![alt](/assets/images/post/ComputerStudy/23.png)

### 3) i - node

- 파일 정류, 접근권한, 하드링크 개수, 소유자의 UID, GID, 파일의 크기, 파일 접근 시각/수정 시각,  
  파일의 i-node 변경 시각 등
- sys/stat.h 파일에 정의되어 있는 **stat 구조체**에 저장

![alt](/assets/images/post/ComputerStudy/24.png)

## 3. 윈도우 파일의 특성

- FAT(File Allocation Table)16, FAT32, NTFS(New Technology File System)의 파일 시스템
- 255자의 긴 파일명 지원
- 파일명과 확장자 사용
