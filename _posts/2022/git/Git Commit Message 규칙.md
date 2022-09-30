---
title: (Git) Commit Message 작성하기 위한 7가지 약속
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Git
description: What is Github
tag: git
article_tag1: git
article_section: git
meta_keywords: git,github,gitcommit
last_modified_at: "2022-09-30 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Git Commit Message 규칙

## 1. Commit Message을 잘 작성해야 하는 이유

- 개발하는 개발자들 입장에서 Commit Message을 보고 현재 브런치 상황을 알아야 하는데 없으면 어려움
- 다른 사람들이 볼 때도 이해하기 쉽다.
- 더 좋은 커밋 로그 가독성
- 더 나은 협업과 리뷰 프로세스
- 더 쉬운 코드 유지보수

## 2. 총 7가지의 Commit Message 규칙

- 제목과 본문을 빈 행으로 구분한다.
- 제목을 50글자 내로 제한
- 제목 첫 글자는 대문자로 작성
- 제목 끝에 마침표 넣지 않기
- 제목은 명령문으로 사용하며 과거형을 사용하지 않는다.
- 본문의 각 행은 72글자 내로 제한
- 어떻게 보다는 무엇과 왜를 설명

## 3. Commit Message 구조

```
    type (타입) : title (제목)
    body (본문, 생략 가능)
    Resolves : #issue, ... (해결한 이슈, 생략 가능)
    See also : #issue, ... (참고 이슈, 생략 가능)
```

### 1) type

- FEAT : 새로운 기능 추가
- FIX : 버그 수정
- DOCS : 문서 수정
- STYLE : 스타일 관련 기능 (코드 포맷팅, 세미콜론 누락, 코드 자체의 변경이 없을 경우)
- REFACTOR : 코드 리펙토링
- TEST : 테스트 코드, 리펙토링 테스트 코드 추가
- CHORE : 빌드 업무 수정, 패키니 매니저 수정 (ex .gitignore 수정 같은 경우)

<a href="https://meetup.toast.com/posts/106">참고한 블로그</a>
