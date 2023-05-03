---
published: true
title: (10분 테크톡) Java 58. DTO vs VO
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-05-03 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# DTO vs VO

## 목차

- DTO란?
- VO란?
- DTO vs VO
- Entity

## 1. DTO 란?

- Data Transfer Object (데이터 전송 객체)
- 계층 (Layer)간 데이터 교환을 위해 사용하는 객ㅊ이다.
- 로직을 갖고 있지 않은 순수한 데이터 객체이며, getter/ setter 메서드만 갖는다.

```java
  public class MoverDto {

    private String source;
    private String target;

    public MoveDto(String source, String target){
      this.source = source;
      this.target = target;
    }

    public String getSource() { return source; }
    public String getTarget() { return target; }
    public void setSource(String source) {this.source = source;}
    public void setTarget(String target) {this.target = target;}
  }
```

## 2. VO 란?

- **Value Object (값 객체)**
- 값 그 자체를 표현하는 객체
- 서로 다른 이름을 가진 VO의 인스턴스가 모든 속성 값이 같다면 같은 객체이다.
- 객체의 불변성을 보장
- 로직을 포함할 수 있음

```java
  public class Color {

    private final double red;
    private final double green;
    private final double blue;

    private Color(double red, double green, double blue){

      this.red = red;
      this.green = green;
      this.blue = blue;
    }

    public static Color of(double res, double green, double blue){
      return new Color(red, green, blue);
    }

    // getter / setter 생략
  }
```

## 3. DTO vs VO

- DTO는 Layer간의 통신 용도로 오고가는 객체
- VO는 특정한 값을 나타내는 객체

## 4. DTO vs VO (cont'd)

- DTO를 VO처럼 불변 객체로 사용하면 얻을 수 있는 이점?
- DTO가 전송하고자 하는 데이터가 전송 과정 중에 변조되지 않음을 보장할 수 있다. (개인적인 결론)

## 5. Entity

- 실제 DB의 테이블과 매핑되는 클래스
- id로 구분된다.
- 로직을 포함할 수 있다.

## 6. Entity (cont'd)

- Entity를 DTO 대신 사용할 수 있지 않을까?

- 사용할 수는 있지만..

- View에서 표현하는 속성 값들이 요청에 따라 계속 달라질 수 있는데, 그때마다 Entity의 속성값을 변경하면 영속성 모델을 표현한 Entity의 순수성이  
  모호해지기 때문에 Controller에서 쓸 DTO와 Entity 클래스는 분리하는게 좋다.

## 출처

<a href="https://www.youtube.com/watch?v=J_Dr6R0Ov8E">라흐의 DTO vs VO</a>
