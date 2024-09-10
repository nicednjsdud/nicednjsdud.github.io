---
title: (Kotlin-Coroutine) 코루틴 이해하기 (1)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Kotlin
description: Kotlin
tag: Kotlin
article_tag1: Kotlin
article_section: Kotlin
meta_keywords: Kotlin, Back_end
last_modified_at: "2024-09-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

## Kotlin 코루틴 (Coroutine) 이해하기

## 1. 코루틴이란?

- Kotlin에서 제공하는 비동기 프로그래밍을 쉽게 구현하기 위한 도구
- 비동기 프로그래밍은 동시에 여러 작업을 처리하거나 대기 시간을 효율적으로 관리할 때 필수적
- 복잡한 비동기 처리 로직을 마치 동기식 코드처럼 간결하게 작성 할 수 있음

## 2. 코루틴과 스레드의 차이점

- 일반적으로 비동기 처리를 할 때는 **스레드(Thread)**를 사용
- 하지만, 스레드는 시스템 리소스를 많이 소비하며, 많은 수의 스레드를 실행하는 것은 비효율적
- 반면, 코루틴은 **경량 스레드**라고 불릴만큼 가벼움
- **코루틴은 하나의 스레드에서 실행되며, 여러 코루틴을 동시에 관리할 수 있어 훨씬 효율적으로 동시성 작업을 처리**

## 3. 코루틴의 동작 원리

- 비동기 작업을 **일시 중단**하고, 나중에 필요할때 다시 **재개**하는 기능을 제공.

```

코루틴 시작 --> 비동기 작업 요청 --> 일시 중단 --> 다른 작업 처리 --> 비동기 작업 완료 후 재개 --> 코루틴 종료

```

1. 코루틴은 시작되면 비동기 작업(예: 네트워크 요청)을 시작합니다.
2. 비동기 작업이 완료될 때까지 코루틴은 중단(suspend) 상태로 들어갑니다.
3. 다른 작업이 완료되면 중단된 코루틴이 **재개(resume)**됩니다.
4. 비동기 작업이 완료되면 코루틴은 종료됩니다.

### 1) 기존 코드 (동기 처리) 예시

- 현재상황 : 동기 처리이기때문에 qna를 가져오고 그다음 comments를 가져옴

```java
class QnaService(
    private val qnaRepository: QnaRepository,
    private val qnaCommentRepository: QnaCommentRepository
) {
    fun getQnaDetails(qnaId: Long): QnaResponse {
        val qna = qnaRepository.findById(qnaId).orElseThrow { throw Exception("Qna not found") }
        val comments = qnaCommentRepository.findByQnaId(qnaId)
        return QnaResponse(qna, comments)
    }
}

```

### 2) 코루틴을 적용한 (비동기 처리) 예시

- 질문(Qna)과 관련된 댓글(QnaComment)을 비동기적으로 가져오도록 변환
- suspend 키워드와 async를 사용하여 비동기 처리를 적용

```java
import kotlinx.coroutines.*

class QnaService(
    private val qnaRepository: QnaRepository,
    private val qnaCommentRepository: QnaCommentRepository
) {
    // suspend 함수로 변환하여 비동기 호출 가능하게 만듦
    suspend fun getQnaDetails(qnaId: Long): QnaResponse = coroutineScope {
        // 비동기로 Qna와 Comments를 가져옴
        val qnaDeferred = async { qnaRepository.findById(qnaId).orElseThrow { throw Exception("Qna not found") } }
        val commentsDeferred = async { qnaCommentRepository.findByQnaId(qnaId) }

        // 결과를 기다리고 반환
        val qna = qnaDeferred.await()
        val comments = commentsDeferred.await()

        return@coroutineScope QnaResponse(qna, comments)
    }
}

```

#### 2-1) suspend 키워드

- **getQnaDetails** 함수가 비동기적으로 동작할 수 있도록 **suspend 키워드를 추가**
- 이를 통해 코루틴 내에서 호출

#### 2-2) @coroutineScope

- 코루틴 내에서 병렬로 여러 작업을 수행하기 위해 **@coroutineScope**를 사용

#### 2-3) async

- qnaRepository와 qnaCommentRepository의 데이터 조회를 비동기적으로 실행하기 위해 async를 사용
- 이는 비동기적으로 데이터베이스 조회를 병렬로 실행하여 성능을 개선할 수 있습니다.

#### 2-4) await

- 각 비동기 작업의 결과를 기다린 후(await), 결과값을 반환
