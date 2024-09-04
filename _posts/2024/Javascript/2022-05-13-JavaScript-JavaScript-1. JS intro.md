---
title: JavaScript 1. JavaScript Intro
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JavaScript
description: JavaScript Intro
tag : JavaScript Basic
article_tag1: JavaScript
article_section: JavaScript
meta_keywords: JavaScript, css, Front-end
last_modified_at: '2022-05-13 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

JavaScript
==========

## JavaScript란?

* 웹 브라우저에서 사용하기 위하여 만들어진 프로그래밍 언어.
* 웹 브라우저 상에서 UI를 동적으로 보여주기 위하여 사용
* Node.js 런타임을 통하여 서버 쪽에서도 사용할 수 있게 됨.
    - Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임.
    - 프로그래밍 언어가 동작하는 환경
    
## 값과 변수 

### 1) 주석

```js
    // 한 줄 메모
    /* 
       여러 줄 메모 
    */
```

### 2) 변수 선언


#### let 키워드

* 변수에 값을 저장함.

```js
    console.log('변수선언')

    et counter = 0
    console.log(counter)

    counter = 'zero'    // 변수 타입변환 가능

    let x   
    console.log(x) // x을 선언하여 값은 undefined라는 특별한 값 할당
```

![alt](/assets/images/post/js/1.png)	

#### const 키워드

* 변수의 값을 절대 바꾸지 않는 상황일때 사용

```js
    const PI = 3.141592
    console.log(PI)
```

![alt](/assets/images/post/js/2.png)

## 데이터 종류(자료형)

### 1) Number (숫자)

* 정수 형식을 따로 제공하지 않음.

```js
    // 문자열을 숫자로 변환
    const PI1 = parseFloat('3.14')
    const PI2 = parseInt('3')
    console.log(typeof PI1,typeof PI2)

    // 숫자를 문자열로 변환
    const PIString1 = PI1.toString()
    const PIString2 = (3).toString()
    console.log(typeof PIString1, typeof PIString2)
```

![alt](/assets/images/post/js/3.png)

## 산술 연산자

## /(나누기) 연산자 

* 연산자와 피연산자가 모두 정수일지라도 항상 부동소수점 수를  
  결과로 반환.

### **(제곱) 연산자

* 제곱 계산

### +=, ++, --

```js

    console.log('1 / 2 : ',1 / 2)
    console.log('2 ** 10 : ', 2 ** 10)
    console.log('2 ** -1 : ', 2 ** -1)
    console.log('(-2) ** 0.5 : ',(-2) ** 0.5)
    console.log('NaN * 0.5 : ',NaN * 0.5)

    let counter = 0
    counter += 10
    console.log('counter+=10 : ',counter)

    counter++
    console.log('counter++ : ', counter)

    counter = 4

    let a = counter++
    let b = ++counter

    console.log('counter : ', counter)
    console.log('a : ',a)
    console.log('b : ',b)
```

![alt](/assets/images/post/js/4.png)

## null과 undefined

* 값의 부재 표현

### undefined 값

* 변수를 선언했지만 초기화 하지 않은 경우.

### null 값

* 의도적인 값의 부재를 의미함.

## 문자열 리터럴

* 작은 따옴표나 큰따옴표로 문자열 리터럴을 감쌈.

```js
    'Hello' 또는 "Hello"
```

## 템플릿 리터럴

* 표현식을 포함 할 수 있다.
* 백틱('')으로 구분함.
* ${....}안의 표현식을 평가한 다음, 필요하면 문자열로 변환되고 템플릿으로  
  합쳐짐
* ${...}표현식 안에 템플릿 리터럴을 중첩할 수 있음.
* 템플릿 리터럴 안의 모든 개행은 문자열에 포함됨

```js
    let myName = "BOB"
    let email = 'BoB@gmail.com'
    let hello = `hello ${myName}`

    console.log(myName)
    console.log(email)
    console.log(hello)

    let BOB = 'world'       // 일반 문자열
    let greeting = `Hello ${BOB.toUpperCase()}` //템플릿 리터럴
    console.log('greeting :',greeting)

    let firstname = '순신'          // 중첩
    let lastname = '이'
    greeting = `Hello, ${firstname.length > 0 ? `
                ${firstname[0]},` : ``}${lastname}`
    console.log('greeting : ',greeting)
```

![alt](/assets/images/post/js/5.png)

## 객체

* 이름/값 또는 프로퍼티의 집합
* 공개 데이터만 포함, 캡슐화 불가능, 동작 포함할 수 없음.
* 자바스크립트 객체는 특정 클래스의 인스턴스가 아님.
* 변수에 객체를 저장할 수 있음.
    * 점 표기법으로 객체 프로퍼티에 접근 가능.
* 기존 프로퍼티의 값을 바꾸거나 새 프로퍼티 추가 가능
* delete 연산자로 프로퍼티 삭제함
    * 존재하지 않는 프로퍼티에 접근하면 undefined가 반환됨.

```js
    const bob = { name: 'bob',age:10}
    console.log('bob: ',bob)

    let bobAge = bob.age
    console.log('bobAge : ',bobAge)

    bob.age = 20
    bob.name = 'Jeong'
    console.log('bob: ',bob)

    delete bob.age
    console.log('bob : ',bob)

    delete bob.age
    console.log('bob : ',bob)

    let name2 = bob.age 
    console.log('name2 :',name2)
```

![alt](/assets/images/post/js/6.png)

## 배열

* '0', '1', '2' 처럼 프로퍼티 이름이 문자열인 객체임
    * 숫자는 프로퍼티 이름으로 사용할 수 없으므로 문자열을 사용함.
* 배열의 요소는 각자 다른 형식을 가질 수 있음.
* 배열은 요소의 값을 갖지 않기도 함.
* 모든 객체에서 존재하지 않는 프로퍼티는 undefined 값을 갖음.
* 배열 끝에 새 요소를 추가할 수 있음.
* 마지막 쉼표는 요소가 누락되었다는 의미가 아님.
    * 시간이 흐르면서 확장될수 있음을 의미함.
* 배열은 객체이므로 필요한 프로퍼티를 배열에 추가할 수 있음.

```js
    const numbers = [1,2,3,'many']
    console.log('numbers : ',numbers)
    console.log(numbers[0])
    console.log(numbers[3])
    console.log(numbers.length)

    const someNumbers = [,2, ,9] // 프로퍼티 '0', '2'에 해당하는 값이 없음
    console.log('someNumbers : ',someNumbers)
    console.log(someNumbers[0])
    console.log(someNumbers[5])

    someNumbers[6] = 11 // someNumbers의 length는 7로 바뀜
    console.log(someNumbers.length)
    console.log(someNumbers)

    const someNumbers2 = [1,2,7,9,]  // 더많은 요소 추가가능 의미
    console.log('someNumber2 :',someNumbers2)
```

![alt](/assets/images/post/js/7.png)

## JSON

* JavaScript Object Notation
* 애플리케이션 간에 객체 데이터를 주고 받는 경량 텍스트 포맷
* 객체, 배열 리터럴을 자바 스크립트 문법으로 표현하는데, 다음 제약이 있음.

### 제약사항

* 객체리터럴, 배열리터럴, 문자열, 소수점 숫자, true, false, null을 값으로  
  사용한다.
* 모든 문자열은 작은따옴표가 이닌 큰따옴표로 구분함.
* 모든 프로퍼티 이름은 큰따옴표로 구분함.
* 맨 끝에 쉼표를 붙일 수 없으며 요소를 생략할 수 없음.

![alt](/assets/images/post/js/8.png)

### JSON 객체의 메소드

#### JSON.stringify(객체, 변환함수, 공백개수)

* 자바스크립트 객체를 문자로 만듦
* 자바스크립트 객체를 JSON 문자열로 변환함

```js
let str = JSON.stringify({name: ['Won young',undefined,'Jeong'], 
                                        age: undefined})
console.log(str)
```

![alt](/assets/images/post/js/10.png)

#### JSON.parse(문자열)

* 문자열을 자바스크립트 객체로 파싱함.

```js
let bob = JSON.parse(
    '{ "name": "Won young Jeong", "age":30 , 
                        "행운의 수": [17, 29], "BOBac":true }'
)

console.log('bob : ',bob)
```

![alt](/assets/images/post/js/9.png)

## 예외란

### try..cahtch..finally 예외처리 기법

```js
    try{
        // 정상적으로 처리되어야 할 코드 기술
        // 코드 실행 중 런타임에서 에러 발생하여 예외가 발생하거나,
    } catch(e){
        // 예외가 발생할 경우에만 실행되는 블록
    } finally {
        // 무조건 실행이 필요한 코드를 이 블록에 기술
    }
```

```js
<script>
    let x = 5
    let result

    try {
        document.writeln('\u2460 <br/>')
        result = x * y
        document.writeln('\u2461 <br/>')
    } catch (e) {
        document.writeln('\u2462' + e + '<br/>')
    } finally {
        document.writeln('\u2463 <br/>')
    }

    document.writeln('<br/>')
</script>
```

![alt](/assets/images/post/js/11.png)
