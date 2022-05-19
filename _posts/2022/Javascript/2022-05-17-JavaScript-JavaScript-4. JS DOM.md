---
title: JavaScript 4. JavaScript DOM
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
last_modified_at: '2022-05-17 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Javascript DOM
================

## 웹 브라우저와 자바스트립트 실행환경

![alt](/assets/images/post/js/13.png)

## 웹 브라우저 객체

### DOM HTML API를 이용한 HTML 문서요소 접근 및 조작

#### 1) 용도 : 문서 순회
##### Node.childNodes
* Node 객체의 배열 객체처럼 작동하는 NodeList 객체로 자식노드  
  객체들에 대한 참조를 갖고 있음.
    - (NodeListOf<ChildNode>)

#### 2) 용도 : 문서 내 요소 찾기

##### Document.getElementById(id)

* id 속성이 같은 유일 노드 객체의 참조를 반환함.

#### 3) 용도 : 문서에 새로운 내용을 추가하기

##### InnerHTML.innerHTML
* HTML 텍스트 문자열을 기술하면 간단히 새로운 내용을 추가함.

```js
      이벤트       이벤트 핸들러 프로퍼티               발생시점
   ------------------------------------------------------------------
    load            onload            문서,이미지 로딩이 완료되었을 때
    abort            onabort           이미지 로딩이 중단되었을 때
    click            onclick           마우스로 클릭할 때
    mousedown        onmousedown       마우스 버튼을 눌렀을 때
    submit           onsubmit          submit 버튼이 눌렸을 때,
                                             (form 내용을 전송)
    change           onchange          요소의 내용이 변경되었을 때

```
## add, cancel 핸들러 등록

```html
    ...
   <meta charset="UTF-8">
    <title>이벤트 핸들러 등록과 이벤트 처리</title>
    <script>

        // 버튼 btnAdd를 클릭하면 이 함수를 호출함.
        function add() {
            // id 속성값이 siteName, siteURL, result인 엘리먼트를 찾아 강조함
            let siteNameElement =document.getElementById('siteName')
            let urlElement = document.getElementById('siteURL') 
            let resultElement = document.getElementById('result')

            // <a> </a> 엘리먼트 생성
            let anchorElement = document.createElement('a')

            // <a href="???"></a> a 엘리먼트의 href 속성값을 urlElement에 저장된 값으로 대입
            anchorElement.href = urlElement.value

            // siteNameElement에 저장된 값으로 텍스트 노드를 생성
            let newTextNode = document.createTextNode(siteNameElement.value)

            // <a></a> 엘리먼트의 자식노드로 방금전 만든 텍스트 노드를 추가함.
            anchorElement.appendChild(newTextNode)

            //<br/> 엘리먼트 생성
            let brElement = document.createElement('br')

            // result 엘리먼트의 자식노드로 anchorElement와 brElement를 추가함
            resultElement.append(anchorElement)
            resultElement.append(brElement)

            // 입력필드 초기화
            siteNameElement.value=''
            urlElement.value=''

        }

        function cancel() {
            // id 속성 값이 siteName,siteURL인 엘리먼트를 찾아 참조
            let siteNameElement =document.getElementById('siteName')
            let urlElement = document.getElementById('siteURL')

            // 입력필드 초기화
            siteNameElement.value=''
            urlElement.value=''
        }

        /* HTML 문서가 파싱되고 외부 컨텐츠 로딩이 완료되면
           웹 브라우저에서는 load 이벤트 발생 */

        /* 이벤트 핸들러로 등록된 함수가 실행됨. */

        /* htmlElement.이벤트 핸들러 프로퍼티명 = function() {  }
           htmlElement.이벤트 핸들러 프로퍼티명 = 함수명*/
        window.onload = function () {
            let btnAddElement = document.getElementById('btnAdd')
            let btnCancel = document.getElementById('btnCancel')
            btnAddElement.onclick = add
            btnCancel.onclick = cancel

        }

    </script>
    ...
```

![alt](/assets/images/post/js/14.png)

## DOM 이벤트 핸들링 
* 이벤트 리스너 (event listener)
* 한개의 HTML 요소에서 복수의 이벤트와 연관을 맺을 수 있음

```html
<title>DOM 이벤트 핸들링</title>
    <script>
        // click 이벤트 발생 시 수행 할 이벤트 핸들러 함수
        function addText() {
            let resultElement = document.getElementById('result')
            resultElement.innerHTML = '이벤트 리스너 구현'
        }

        // click 이벤트 발생 시 수행 할 이벤트 핸들러 함수
        function clearText() {
            let resultElement = document.getElementById('result')
            resultElement.innerHTML = ''
        }
        // load 이벤트 발생 시 수행할 이벤트 핸들러 함수
        function init(){
            /* id 속성 값 btnClick, btnCancel 인 버튼을 찾아
                이벤트 리스너 등록 함수를 사용해 click 이벤트
               핸들러 함수를 등록*/
            let btnClickElement = document.getElementById('btnClick')
            let btnCancelElement = document.getElementById('btnCancel')

            addListener(btnClickElement,'click', addText)
            addListener(btnCancelElement,'click', clearText)
        }
        /* 크로스 브라우징 고려한 이벤트 리스너 등록 함수
            el : 이벤트가 발생한 HTML 요소
            ev : 이벤트
            handler : 이벤트 핸들러 함수
         */
        function addListener(el, ev, handler){
            el.addEventListener(ev,handler,false)


        }

        addListener(window, 'load', init)
    </script>
</head>
<body>
<form>
    <input type="button" id="btnClick" value="눌러주세요"/>
    <input type="button" id="btnCancel" value="취소"/>
</form>
<div>
    <div id="result">

    </div>
</div>
</body>
```

![alt](/assets/images/post/js/15.png)
![alt](/assets/images/post/js/16.png)