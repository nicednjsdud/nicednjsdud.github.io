---
published: true
title: "디스크 접근 시간(Disk Access Time)의 이해와 성능 분석"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
description: "디스크에서 데이터를 읽는 데 걸리는 시간, 즉 디스크 접근 시간의 구성 요소와 성능 최적화를 위한 주요 개념을 정리합니다."
tag: [Disk Access Time, OS, Seek Time, Rotational Latency, Transfer Time, Random Access, Sequential Access]
article_section: "OS"
meta_keywords: "Disk Access Time, Seek Time, Rotational Latency, Transfer Time, 디스크 접근 시간, 랜덤 액세스, 순차 액세스"
last_modified_at: "2025-05-30 21:55:00 +0900"
toc: true
toc_sticky: true
toc_label: "목차"
---

## 💾 디스크 접근 시간이란?

디스크 접근 시간(Disk Access Time)은 디스크에서 데이터를 읽거나 쓸 때 걸리는 전체 시간을 의미합니다. 이는 크게 **탐색 시간(Seek Time)**, **회전 지연 시간(Rotational Latency)**, **데이터 전송 시간(Data Transfer Time)**의 세 가지로 구성됩니다.

---

## 🧩 디스크 접근 시간의 구성 요소

### 1. 탐색 시간 (Seek Time)
- 디스크 헤드가 데이터를 읽기 위해 해당 **트랙(track)** 으로 이동하는 데 걸리는 시간입니다.
- 기계적인 움직임이 수반되며, 물리적인 이동 거리가 짧을수록 빠릅니다.
- **지역성(Locality)** 이 높은 경우 탐색 시간이 단축됩니다.

### 2. 회전 지연 시간 (Rotational Latency)
- 디스크가 회전하면서 **읽고자 하는 섹터가 디스크 헤드 아래로 도달하기까지 걸리는 시간**입니다.
- 평균 회전 지연 시간은 디스크의 회전 속도에 반비례합니다.

### 3. 데이터 전송 시간 (Data Transfer Time)
- 실제 데이터를 디스크에서 메모리로 전송하는 시간입니다.
- 전송 속도는 회전 속도, 트랙 밀도, 버스 전송률 등에 따라 달라집니다.

---

## 🔄 랜덤 액세스 vs 순차 액세스

| 구분 | 랜덤 액세스 (Random Access) | 순차 액세스 (Sequential Access) |
|------|------------------------------|-----------------------------------|
| 정의 | 데이터가 서로 떨어져 있는 위치에 저장 | 데이터가 연속된 위치에 저장 |
| 성능 | 느림 (헤드 이동 + 회전 지연 반복) | 빠름 (헤드 이동 거의 없음) |
| 예시 | DB 인덱스 탐색, 랜덤 파일 읽기 | 로그 저장, 스트리밍 처리 |

**💡 정리:** 디스크의 물리적 구조로 인해 순차 액세스는 랜덤 액세스보다 훨씬 빠릅니다.

---

## ✅ 백엔드 개발자가 알아야 할 점

- 디스크 접근 시간은 성능 병목의 주요 원인이 될 수 있습니다.
- 데이터베이스에서 인덱스를 잘 설계하거나, **순차적인 I/O를 유도하는 로직 설계**가 중요합니다.
- SSD는 구조상 탐색 및 회전 지연이 없으므로, 이 개념은 **HDD 기반 시스템에 더욱 중요**합니다.
