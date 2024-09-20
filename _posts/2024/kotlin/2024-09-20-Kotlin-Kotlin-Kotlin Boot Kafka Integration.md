---
title: (Kotlin-Kafka) Kotlin Spring Boot Kafka 통합 초기 세팅
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
last_modified_at: "2024-09-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

## Kotlin 코루틴 (Coroutine) 이해하기 - 2

- Kotlin에서 Spring Boot를 사용하여 Kafka와 통합하는 방법

## 목차

1. Kafka Dependencies 설정
2. application.yml 설정
3. KafkaConfig 설정
4. Consumer 구현
5. Producer 구현

## 1. Kafka Dependencies 설정

```kotlin
dependencies {
    implementation("org.springframework.kafka:spring-kafka")
    implementation("com.fasterxml.jackson.module:jackson-module-kotlin")
    testImplementation("org.springframework.kafka:spring-kafka-test")
}
```

## 2. appication.yml 설정

- 이 파일은 Kafka 클러스터에 연결하기 위한 서버 주소, 토픽 이름, 그룹 ID 등을 설정합니다.

```yaml
spring:
  kafka:
    bootstrap-servers: kafka:9092
    consumer:
      group-id: board-service-group
      auto-offset-reset: earliest
      key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
      value-deserializer: org.springframework.kafka.support.serializer.JsonDeserializer
      properties:
        spring.json.trusted.packages: "*"
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.springframework.kafka.support.serializer.JsonSerializer
```

### 1) bootstrap-servers

- Kafka 브로커 주소입니다.

### 2) group-id

- Consumer가 속한 그룹 ID입니다.

### 3) auto-offset-reset

- 컨슈머가 없는 상태에서 새로운 Consumer가 구독을 시작할 때 처음부터(earliest) 메시지를 소비할지,  
  가장 최신(latest) 메시지만 소비할지 결정합니다.

### 4) key-serializer/value-serializer

- Producer가 메시지를 직렬화할 때 사용하는 Serializer입니다.

### 5) key-deserializer/value-deserializer

- Consumer가 메시지를 역직렬화할 때 사용하는 Deserializer입니다.

## 3. KafkaConfig 설정

- Kafka의 Consumer와 Producer를 설정하기 위해 KafkaConfig 클래스를 생성
- 이 클래스에서는 **ConcurrentKafkaListenerContainerFactory**를 설정하여  
  Consumer 메시지를 처리할 수 있도록 설정합니다.

### KafkaConfig.kt

```kotlin
import org.apache.kafka.clients.consumer.ConsumerConfig
import org.apache.kafka.clients.producer.ProducerConfig
import org.apache.kafka.common.serialization.StringDeserializer
import org.apache.kafka.common.serialization.StringSerializer
import org.springframework.beans.factory.annotation.Value
import org.springframework.context.annotation.Bean
import org.springframework.context.annotation.Configuration
import org.springframework.kafka.annotation.EnableKafka
import org.springframework.kafka.config.ConcurrentKafkaListenerContainerFactory
import org.springframework.kafka.core.*
import org.springframework.kafka.support.serializer.JsonDeserializer
import org.springframework.kafka.support.serializer.JsonSerializer

@EnableKafka
@Configuration
class KafkaConfig {

    @Value("\${spring.kafka.bootstrap-servers}")
    private val BOOTSTRAP_SERVER: String? = null

    @Value("\${spring.kafka.consumer.group-id}")
    private val GROUP_ID: String? = null

    @Value("\${spring.kafka.consumer.auto-offset-reset}")
    private val AUTO_OFFSET_RESET: String? = null

    // Consumer 설정을 위한 Factory Bean을 정의합니다.
    // 여러 개의 Consumer 스레드를 설정하기 위해 setConcurrency를 사용하여 동시성을 3으로 설정합니다.
    @Bean
    fun kafkaListenerContainerFactory(): ConcurrentKafkaListenerContainerFactory<String, Any> {
        val factory = ConcurrentKafkaListenerContainerFactory<String, Any>()
        factory.consumerFactory = consumerFactory()
        factory.setConcurrency(3)
        return factory
    }

    // Consumer 설정
    @Bean
    fun consumerFactory(): ConsumerFactory<String, Any> {
        val deserializer = JsonDeserializer(Any::class.java)
        deserializer.addTrustedPackages("*")

        val config = mapOf(
            ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG to BOOTSTRAP_SERVER,
            ConsumerConfig.GROUP_ID_CONFIG to GROUP_ID,
            ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG to StringDeserializer::class.java,
            ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG to deserializer,
            ConsumerConfig.AUTO_OFFSET_RESET_CONFIG to AUTO_OFFSET_RESET
        )
        return DefaultKafkaConsumerFactory(config, StringDeserializer(), deserializer)
    }

    // Producer 설정을 위한 Factory Bean을 정의합니다.
    @Bean
    fun producerFactory(): ProducerFactory<String, Any> {
        val config = mapOf(
            ProducerConfig.BOOTSTRAP_SERVERS_CONFIG to BOOTSTRAP_SERVER,
            ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG to StringSerializer::class.java,
            ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG to JsonSerializer::class.java
        )
        return DefaultKafkaProducerFactory(config)
    }

    @Bean
    fun kafkaTemplate(): KafkaTemplate<String, Any> {
        return KafkaTemplate(producerFactory())
    }
}


```

## 4. Kakfa Consumer 구현

- Kafka의 메시지를 수신하고 처리하는 Consumer는 `@KafkaListener`를 통해 구현할 수 있습니다.

```kotlin

ipackage brn.neos.neos_board_backend.kafka.listener
import org.apache.kafka.clients.consumer.ConsumerRecord
import org.springframework.kafka.annotation.KafkaListener
import org.springframework.stereotype.Service

@Service
class TopicUserListener() {
    val log = LoggerFactory.getLogger(TopicUserListener::class.java)

    // Kafka로부터 "user-join" 토픽을 구독하는 Consumer 메서드
    @KafkaListener(topics = ["user-join"])
    fun consumeConfirmUser(message: ConsumerRecord<String, Map<String, Any>>) {
        // 처리 로직
    }

    // Kafka로부터 "user-join-rollback" 토픽을 구독하는 Consumer 메서드
    @KafkaListener(topics = ["user-join-rollback"])
    fun consumeRollBackUser(message: ConsumerRecord<String, Map<String, Any>>) {
        // 처리 로직
    }
}

```

### 5. Kafka Producer 구현

- Kafka에 result 메세지를 목적으로 Producer를 구현했습니다.
- 서버끼리 메시지를 맞춰서 보내면 됩니다.
- 밑 코드는 `$토믹-result`에 보내는 코드입니다.

### 1) 데이터 예시

```json
    "test_id" : "test",
    "data" : {
        "test_id" to message.test_id,
        "service" to "BOARD_SERVICE",
        "event" to topic,
        "data" to message.data,
        "status" to status
    }
```

### 2) 구현

```
import com.fasterxml.jackson.module.kotlin.jacksonObjectMapper
import org.springframework.kafka.core.KafkaTemplate
import org.springframework.stereotype.Component

@Component
class KafkaMessageUtils(
    private val kafkaTemplate: KafkaTemplate<String, Any>
) {

    fun <T> messageFormatter(value: Map<String, Any>, type: Class<T>): Message<T> {
        val objectMapper = jacksonObjectMapper()
        val constructParametricType = objectMapper.typeFactory.constructParametricType(Message::class.java, type)
        return objectMapper.readValue(objectMapper.writeValueAsString(value), constructParametricType)
    }

    fun sendResultMessage(message: Message<*>, topic: String, status: String) {
        val messageData = mapOf(
            "test_id" to message.test_id,
            "service" to "BOARD_SERVICE",
            "event" to topic,
            "data" to message.data,
            "status" to status

        )
        kafkaTemplate.send("$topic-result", messageData)
    }

    data class Message<T>(
        val test_id: String,
        val data: T
    )
}

```
