---
title: JavaScript 5. jQuery
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- JavaScript
description: jQuery
tag : JavaScript Basic
article_tag1: JavaScript
article_section: JavaScript
meta_keywords: JavaScript, css, Front-end
last_modified_at: '2022-05-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

jQuery
========

![alt](/assets/images/post/js/17.png)

## jQuery

* DOM의 쉬운 조작, 쉽고 일관된 이벤트 처리, 각종 효과 기능 제공  
  (시각화 지원), 쉬운 Ajax 지원등 자바스크립트 전반을 지원하는  
  라이브러리(프레임 워크)
* 자바스크립트에서 DOM 객체를 질의(query)해 조작한다는 의미

```
    => 문서 탐색 및 조작을 위한 쉬운 노드 접근 기술 제공.
```

* HTML DOM 객체에 접근하기 위해 셀렉터(selector) 매커니즘을 사용

```
    - CSS 셀렉터로 문서의 특정 노드를 찾을 수 있음.
```

## $() , jQuery()

* HTML DOM의 특정 노드에 접근하거나, DOM 요소를 생성하거나,DOM 구조의  
   로딩을 완료한 후 실행할 콜백함수를 지정하기 위해 사용하는 함수

* jQuery 객체의 메소드는 jQuery 객체 자신을 반환 값으로 전달하기 떄문에  
  메소드 체인 구성이 가능.

### ()안에 매개변수로 셀렉터를 기술 

* 셀렉터를 해석해 HTML DOM 구조 상의 노드를 찾아 jQuery 객체로 반환함.
* 해당 객체와 이벤트를 바인딩(연결)하거나, 효과를 연결하는 작업이 가능.

### $

* jQuery의 별칭  

## jQuery(document).ready(function(){...})

* == $(document).ready(function(){...})
* jQuery 이벤트인 문서 로딩 이벤트에 대한 이벤트 핸들러 구현할때 사용.

```
    - 매개변수로 전달된 document 객체를 jQuery 객체로 변환하고,
      jQuery 객체의 ready() 메소드의 매개변수인 함수가 문서 로딩  
      이벤트의 이벤트 핸들러 함수로 등록됨.
```

### id에 해당하는 요소에 클래스만들기

![alt](/assets/images/post/js/18.png)
![alt](/assets/images/post/js/19.png)


## 셀렉터

* 문서 내의 노드를 쉽게 식별하고 참조하기 위해 사용하는 기술
* CSS 셀렉터와 동일

```js
        ...
     // parent > child (parent 요소의 자식요소를 선택)
            $('#list > div:nth-child(2n)').addClass('evenitem')
            $('#list > div:nth-child(2n+1)').addClass('odditem')

            let $element =$('#list > div')

            $('#message').text('앞으로 강좌' + $element.length+'강')

            let resultStr =''

            $('<h4>강좌</h4>').appendTo('#result')
            $element.each(function (index,element){
                resultStr = (index+1) +'.'+$(element).text()
                $('#result').append(resultStr)
                $('#result').append('<br/>')
            })
        ...
```

![alt](/assets/images/post/js/20.png)

## jQuery 이벤트 종류

```
    1. 문서 로딩            ready       해당 DOM 로딩이 완료되었을 때
    2. 마우스              click
                         dbclock
                         focusin
                         focusout
                         hover
                         mouseenter
                         mouseleave
                         mousedown
                         mouseup
                         mousemove
                         mouseout
                         mouseover

    3. 키보드             keypress
                         keydown
                         keyup
                         focusin
                         focusout

    4. form              focus
                         blur
                         change
                         select
                         submit

    5. 웹브라우저          resize
                         scroll
```

## 이벤트 등록 및 제거
### on()
* 현재 선택된 요소에 대해 하나 이상의 이벤트와 이벤트 핸들러 함수를   
  연결하는 메서드

### off()
* 현재 선택된 요소에 대해 하나 이상의 이벤트와 이벤트 핸들러 함수를   
  연결을 제거하는 메서드

### one()
* 현재 선택된 요소에 대해 하나이상의 이벤트와 이벤트 핸들러 함수를   
  연결하는 메서드이나, 한 번만 실행.




## 요소를 보이거나 감추는 기능

### hide()
* 요소가 사라지는 애니메이션 효과를 주기 위해 사용
* 애니메이션의 실해되는 시간 설정 (문자열 or 숫자 값)
    - 'slow', 'normal', 'fast'
    - 200, 400, 600
#### call back 함수
* 애니메이션이 끝났을 때 호출되는 함수임
### show()
* 요소가 나타나는 애니메이션 효과를 주기 위해 사용

```js
    ...
 <style>
        .test {color : #000; padding: .5em; border :1px solid #444; }
        .active { color: #900; font-weight: bold; }
        .inside { background-color:aqua;}
    </style>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
    <script>
        $(document).ready(function (){
            // on메서드
            $("div.test").on({
                click: function () {
                    $(this).toggleClass("active")
                },
                mouseenter: function () {
                    $(this).addClass("inside")
                    $(this).text("mouseenter")
                },
                mouseleave:function () {
                    $(this).removeClass("inside")
                    $(this).text("mouseleave")
                }
            })
        })
    </script>
    ...
```

* 하나씩 보이기

![alt](/assets/images/post/js/21.png)

* 하나씩 감추기

![alt](/assets/images/post/js/22.png)

## 페이딩

* HTML 요소의 불투명도(opacity)를 조정하는 기능

### fadeIn()
* opacity를 0에서 1로 변경하여 서서히 나타나는 애니메이션 효과를 주기 위해 사용

### fadeOut()
* opacity를 1에서 0으로 변경하여 서서히 사라지는 애니메이션 효과를 주기 위해 사용

```js
    ...
 <script>
        $(document).ready(function () {
            $("#fadein").click(function () {
                $("#image").fadeIn(3000)
            })
            $("#fadeout").click(function () {
                $("#image").fadeOut(3000)
            })
        })

    </script>
</head>
<body>
    <div class="picframe">
        <img src="alaskan_malamute.jpg" id="image">
    </div>
    <div>
        <button id="fadein">페이드인</button>
        <button id="fadeout">페이드아웃</button>
    </div>
    ...
```

* 3초 간격으로 사라지거나 나타남

![alt](/assets/images/post/js/23.png)

## 슬라이딩

* HTML 요소의 높이를 조절하여 접었다 폈다 할 수 잇는 기능
* slideUp()
* slideDown()

```js
    ...
    $('.submenuitem').hide()
            $('div .menuitem').bind('click',function () {
                if($(this).next().css('display')==='none'){
                    $('.submenuitem').slideUp()
                }
                $(this).next().slideDown()
            })
    ```
```

![alt](/assets/images/post/js/24.png)

