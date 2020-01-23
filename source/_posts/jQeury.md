---
title: jQuery
date: 2017-08-16 13:11:01
tags:
  - jQuery
category:
  - web
  - jQuery
---

# 기본

- jQuery = 자바스크립트 라이브러리
  라이브러리 = 편리하게 사용할 수 있는 객체, 함수 등의 집합

- jQuery의 목적 = "쉽게"
  문서 객체 모델과 관련된 처리를 "쉽게" 구현
  일관된 이벤트 연결을 "쉽게" 구현
  시각적 효과를 "쉽게" 구현
  Ajax 애플리케이션을 "쉽게" 개발

## jQuery 사용법

    직접 다운로드 or CDN 호스트 사용
    CDN = Content Delivery Network = Content Distribution Network = 웹 링크

```html
//로컬에 저장
<script src="jquery-3.1.1.js"></script>
//웹 링크
<script
  src="https://code.jquery.com/jquery-3.1.1.js"
  integrity="sha256-16cdPddA6VdVInumRGo6IbivbERE8p7CQR3HzTBuELA="
  crossorigin="anonymous"
></script>
```

## SRI 해시(Subresource Integrity Hash)

XSS방어를 위한 CDN의 intergiry속성과 crossorigin속성
js파일이 jQuery 사이트에서 정식으로 제공된건지 무결성 검사
OO.js = Unconpressed 버전(용량 5배 이상)
OO.min.js = Minified 버전

## \$란?

jQuery.js의 코드를 보면 다음 부분이 있다.
`window.jQuery = window.$ = jQuery;`
결국 jQuery 식별자를 \$로 대처한 것임

## jQuery 코드의 시작

| 메서드                | 기능                                           |
| --------------------- | ---------------------------------------------- |
| `$(docuemnt).ready()` | 문서가 준비되면 매개변수로 넣은 콜백 함수 실행 |

JS의 다음과 같음

```javascript
window.onload = function() {};
```

간편하게 아래와 같이도 씀

```javascript
$(function() {});
```

고전 이벤트 모델과 달리. 표준 이벤트 모델이나 IE 이벤트 모델과 마찬가지로
복수 개의 이벤트를 연결할 수 있음 => 실행시키면 연달아 3개 alert됨

```javascript
$(docuemnt).ready(function() {
  alert("First");
});
$(docuemnt).ready(function() {
  alert("Second");
});
$(docuemnt).ready(function() {
  alert("Third");
});
```

## 기본 선택자

기본 형태

```javascript
$("h1").css("color", "red"); //선택하고 메서드 붙여 사용
```

선택자

| 메서드            | 기능          |
| ----------------- | ------------- |
| \$('\*')          | 전체 선택자   |
| \$('태그이름')    | 태그 선택자   |
| \$('#아이디이름') | 아이디 선택자 |
| \$('.클래스이름') | 클래스 선택자 |

여러 개의 태그 선택

```javascript
$("h1", "p");
```

h1 태그면서 id속성이 target인 문서 객체 선택

```javascript
$("h1#targe");
```

두 개 이상의 클래스를 한 번에 갖는 문서 객체 선택

```html
<script>
  $(".item.select");
</script>

<div class="item"></div>
//선택
<div class="item select"></div>
<div class="item"></div>
```

## 자손 선택자

자손 = 직속 하위 단계

| 메서드            | 기능        |
| ----------------- | ----------- |
| \$('부모 > 자손') | 자손 선택자 |

## 후손 선택자

    후손 = 모든 하위 단계

| 메서드          | 기능        |
| --------------- | ----------- |
| \$('부모 후손') | 후손 선택자 |

## 속성 선택자

| 메서드               | 기능                                                      |
| -------------------- | --------------------------------------------------------- |
| \$('요소[속성=값]')  | 속성과 값이 같은 문서 객체를 선택                         |
| \$('요소[속성=값]')  | 속성 안의 값이 특정 값과 같은 문서 객체를 선택            |
| \$('요소[속성~=값]') | 속성 안의 값이 특정 값을 단어로 시작하는 문서 객체를 선택 |
| \$('요소[속성^=값]') | 속성 안의 값이 특정 값으로 시작하는 문서 객체를 선택      |
| $('요소[속성$=값]')  | 속성 안의 값이 특정 값으로 끝나는 문서 객체를 선택        |
| \$('요소[속성*=값]') | 속성 안의 값이 특정 값을 포함하는 문서 객체를 선택        |

```html
<script>
  $(document).ready(function() {
    $('input[type="text"]').val("텍스트를 여기에 입력");
  });
</script>
<body>
  <input type="text" />
</body>
```

## 필터 선택자

**입력 양식 필터 선택자1**
input의 type속성에 따라 문서 객체를 선택(속성 선택자랑 같은 기능이지만 사용법이 간단함)

| 메서드              | 기능                                                              |
| ------------------- | ----------------------------------------------------------------- |
| \$('요소:button')   | input 태그 중 type 속성이 button인 문서 객체와 button 태그를 선택 |
| \$('요소:checkbox') | input 태그 중 type 속성이 check인 문서 객체를 선택                |
| \$('요소:file')     | input 태그 중 type 속성이 file인 문서 객체를 선택                 |
| \$('요소:image')    | input 태그 중 type 속성이 image인 문서 객체를 선택                |
| \$('요소:password') | input 태그 중 type 속성이 password인 문서 객체를 선택             |
| \$('요소:radio')    | input 태그 중 type 속성이 radio인 문서 객체를 선택                |
| \$('요소:reset')    | input 태그 중 type 속성이 reset인 문서 객체를 선택                |
| \$('요소:submit')   | input 태그 중 type 속성이 submit인 문서 객체를 선택               |
| \$('요소:text')     | input 태그 중 type 속성이 text인 문서 객체를 선택                 |

**입력 양식 필터 선택자2**

| 메서드              | 기능                                                       |
| ------------------- | ---------------------------------------------------------- |
| \$('요소:checked')  | 체크되어 있는 입력 양식을 선택                             |
| \$('요소:disabled') | 비활성화된 입력 양식을 선택                                |
| \$('요소:enabled')  | 활성화된 입력 양식을 선택                                  |
| \$('요소:focus')    | 초점이 맞추어져 있는 입력 양식을 선택                      |
| \$('요소:input')    | 모든 입력 양식을 선택(input, textarea, select, button)     |
| \$('요소:selected') | option 객체 중 선택된 태그를 선택 //사실상 option:selected |

```html
<script>
  $(document).ready(function() {
    setTimeout(function() {
      var value = $("select > option:selected").val();
      alert(value); // B!! 출력
    }, 5000); //5초 후 함수 실행
  });
</script>
<body>
  <select>
    <option>A!!</option>
    <option>B!!</option>
    //선택되었을 때
    <option>C!!</option>
  </select>
</body>
```

**위치 필터 선택자**

| 메서드           | 기능                                |
| ---------------- | ----------------------------------- |
| \$('요소:odd')   | 홀수 번째에 위치한 문서 객체를 선택 |
| \$('요소:even')  | 짝수 번째에 위치한 문서 객체를 선택 |
| \$('요소:first') | 첫 번째에 위치한 문서 객체를 선택   |
| \$('요소:last')  | 마지막에 위치한 문서 객체를 선택    |

```html
// 이런 table이 위치 필터를 활용하기 좋음
<table>
  <tr>
    <th>항목1</th>
    <th>항목2</th>
  </tr>
  <tr>
    <td>항목1</td>
    <td>항목2</td>
  </tr>
  <tr>
    <td>항목1</td>
    <td>항목2</td>
  </tr>
  <tr>
    <td>항목1</td>
    <td>항목2</td>
  </tr>
  <tr>
    <td>항목1</td>
    <td>항목2</td>
  </tr>
</table>
```

**함수 필터 선택자**

| 메서드                      | 기능                                    |
| --------------------------- | --------------------------------------- |
| \$('요소:contains(문자열)') | 특정 문자열을 포함하는 문서 객체를 선택 |
| \$('요소:eq(n)')            | n번째 위치하는 문서 객체를 선택         |
| \$('요소:gt(n)')            | n번째 초과에 위치하는 문서 객체를 선택  |
| \$('요소:lt(n)')            | n번째 미만에 위치하는 문서 객체를 선택  |
| \$('요소:has(h1)')          | h1 태그가 있는 문서 객체를 선택         |
| \$('요소:not(선택자)')      | 선택자와 일치하지 않는 문서 객체를 선택 |
| \$('요소:nth-child(3n+1)')  | 3n+1번째에 위치하는 문서 객체를 선택    |

<table>에 함수 필터를 활용하기 좋음

## 배열 관리

| 메서드    | 기능                                                                     |
| --------- | ------------------------------------------------------------------------ |
| \$.each() | for in 반복문처럼 객체나 배열의 요소를 검사하는 메서드, AJAX에서 많이 씀 |

| 메서드                                    |
| ----------------------------------------- |
| \$.each(object.function(index, item){})   |
| \$(selector).each(function(index,item){}) |

index = 배열의 인덱스, 객체의 키
item = 해당 인덱스나 키가 가진 값

ECMAScript5에서 추가된 forEach() 메서드와 매개변수 순서가 다름(주의)

| 메서드                               |
| ------------------------------------ |
| [].forEach(function(item, index){}); |

**JavaScript의 배열 관리**

```html
<script>
  //배열 선언하고
  var array = [
    { name: "네이버", link: "www.naver.com" },
    { name: "다음", link: "www.daum.net" },
    { name: "한빛미디어", link: "www.hanbit.co.kr" }
  ];
  //각각의 배열에 대해 콜백함수 실행
  $.each(array, function(index, item) {
    var output = "";
    output += "<a href='" + item.link + "'>";
    output += "<h1>" + item.name + "</h1>";
    output += "</a>";
    document.body.innerHTML += output;
  });
</script>
```

**jQuery의 배열 관리**

```html
<style>
  .color-0 {
    background: green;
  }
  .color-1 {
    background: yellow;
  }
  .color-2 {
    background: red;
  }
</style>
<script>
  $(document).ready(function() {
    //복수개의 태그가 선택될 때 이 메서드 씀
    $("h1").each(function(index, item) {
      //각각의 item이 객체 자체이므로 내장함수 사용 가능, item 대신 this 사용가능
      $(item).addClass("color-" + index);
    });
  });
</script>
<body>
  <h1>JavaScript</h1>
  <h1>ReactJS</h1>
  <h1>NodeJS</h1>
</body>
```

## 객체 확장

| 메서드                                       | 기능                               |
| -------------------------------------------- | ---------------------------------- |
| \$.extend(object, addObject, addObject, ...) | 2번째부터의 객체들을 object에 붙임 |

```html
<script>
  $(document).ready(function() {
    var object = {};
    //기존의 방법
    object.name = "김용훈";
    //메서드 사용하는 방법
    $.extend(object, {
      age: 24,
      major: "informatics"
    });
  });
</script>
```

## jQuery 충돌 방지

jQuery 이외에도 다양한 JavaScript 프레임워크들이 있다.
여러 플러그인을 함께 사용할 때는 플러그인 간의 충돌이 발생할 수 있다.
예를 들어 Prototype 프레임워크도 식별자 \$를 사용한다.

| 메서드          | 기능                                        |
| --------------- | ------------------------------------------- |
| \$.noConflict() | jQuery의 식별자 \$를 더 이상 사용할 수 없음 |

```html
<script>
  $.noConflict(); //기본 식별자 jQuery를 사용해야함
  jQuery(document).ready(function() {});
</script>
```

간단하게 쓰고 싶으면 "var J = jQuery;" 선언으로 J를 식별자로 사용할 수 있음

| 메서드      | 기능                           |
| ----------- | ------------------------------ |
| \$.extend() | 메서드를 사용한 옵션 객체 보완 |

1. 짧은 조건문을 사용하여 매개변수로 전달된 객체의 값 보완

```html
<script>
  function test(options) {
    options.valueA = options.valueA || 10;
    options.valueB = options.valueB || 20;
    options.valueC = options.valueC || 30;

    alert(options.valueA + " : " + options.valueB + " : " + options.valueC);
  }
  test({}); // 10 : 20 : 30 출력
  test({
    valueA: 52,
    valueC: 273
  }); // 52 : 20 : 273 출력
</script>
```

2. \$.extend(기본값 객체, 사용자 정의 객체, ...)를 활용하여 객체의 값 보완

```html
<script>
  //위 function과 같은 기능을 함
  function test(options) {
    options = $.extend({ valueA: 10, valueB: 20, valueC: 30 }, options);
    alert(options.valueA + " : " + options.valueB + " : " + options.valueC);
  }
</script>
```

# 문서 객체 선택과 탐색

## 기본 필터 메서드

jQuery의 선택자를 사용하면 원하는 문서 객체를 대부분 선택할 수 있으나
기본적으로 지원하지 않는 필터로 문서 객체를 선택해야 한다면 다음 메서드 사용

| 메서드   | 기능               |
| -------- | ------------------ |
| filter() | 문서 객체를 필터링 |

```html
<script>
  $(selector)
    .filter(selector)
    .메서드();
  $(selector)
    .filter(function() {})
    .메서드();
</script>
<body>
  <h3>Header-0</h3>
  -> index 0
  <h3>Header-1</h3>
  -> index 1
  <h3>Header-2</h3>
  -> index 2
  <h3>Header-3</h3>
  -> index 3
</body>
<script>
  $("h3").filter(:even).메서드(); //짝수번째 선택
  $("h3").filter(
   //3의 배수 선택
   function(index){return index % 3 == 0;}
  ).메서드();
</script>
```

## 객체 선택 메서드 체이닝

`$('h3:even')` 말고 굳이 필터 메서드를 사용하여 `$('h3').filter(:even)` 로 하는 이유 = 범위의 문제

```html
<script>
  $("h1")
    .css("background", "orange")
    .filter(":even")
    .css("color", "red");
  //모든 h1에 배경을 먹이고 짝수 h1에 글씨색을 먹임
</script>
```

| 메서드 | 기능                               |
| ------ | ---------------------------------- |
| end()  | 문서 객체 선택을 한 단계 뒤로 돌림 |

```html
<script>
  $('h1').css('background', 'orange');
  $('h1:even').css('color', 'white');
  $('h1:odd').css('color', 'red');

  $('h1').css().filter(:even).css().filter(:odd).css(); //연달아 체이닝 해버리면 odd가 even의 하위로 들어감
  $('h1').css().filter(:even).css().end().filter(:odd).css(); //even과 odd를 같은 깊이에 놓으려면 even에서 end()로 트리 상위로 한단계 올라갔다가 다시 내려와야함
</script>
```

## 특정 위치의 문서 객체 선택

`$('h1').메서드()` => 선택된 인덱스들 중에서 특정 위치의 문서객체 선택

| 메서드  | 기능                                  |
| ------- | ------------------------------------- |
| eq()    | 특정 위치에 존재하는 문서 객체를 선택 |
| first() | 첫 번째에 위치하는 문서 객체를 선택   |
| last()  | 마지막에 위치하는 문서 객체를 선택    |

```html
<h1></h1>
-> eq(0), eq(-3), first()

<h1></h1>
-> eq(1), eq(-2)

<h1></h1>
-> eq(2), eq(-1), last()
```

## 문서 객체 추가 선택

| 메서드 | 기능                        |
| ------ | --------------------------- |
| add()  | 문서 객체를 추가적으로 선택 |

메서드 체이닝에 유용하게 쓰임

```html
<h1></h1>
<h2></h2>
<h1></h1>
<h2></h2>
<script>
  $("h1")
    .css("color", "white")
    .add("h2")
    .css("float", "left");
  //->흰글씨, 검은글씨, 흰글씨, 검은글씨 순으로 float left됨
</script>
```

## 문서 객체의 특징 판별

| 메서드 | 기능                  |
| ------ | --------------------- |
| is()   | 문서 객체의 특징 판별 |

```html
<script>
  $("h1").each(function() {
    if ($(this).is(".select")) {
      //boolean 반환
      $(this).css();
    }
  });
</script>
```

## 특정 태그 선택

| 메서드 | 기능                                      |
| ------ | ----------------------------------------- |
| find() | 특정 태그를 선택, XML문서 파싱에 유용하다 |

보통 Ajax로 서버에서 XML 문서를 가져오지만, 문자열로 직접 쓰면 이렇게 됨

```javascript
var xml = "<friends><friend><name>김우식</name><pr>father</pr></friend>";
xml += "<friend><name>한재연</name><pr>mom</pr></friend>";
xml += "<friend><name>김유림</name><pr>sister</pr></friend></friends>";

//문자열을 XML 문서 객체로 변경
var xmlDoc = $.parseXML(xml);

//이 XML 문서를 파싱
$(xmlDoc)
  .find("friend")
  .each(function(index) {
    var output = "<div>";
    output +=
      "<h1>" +
      $(this)
        .find("name")
        .text() +
      "</h1>";
    output +=
      "<h1>" +
      \$(this)
        .find("pr")
        .text() +
      "</h1>";
    output += "</div>";
    document.body.innerHTML += output;
  });
```

## 특정 태그의 부모 태그 선택

| 메서드   | 기능                       |
| -------- | -------------------------- |
| parent() | 특정 태그의 부모 태그 선택 |

```html
<div><h1>배경 바꾸기</h1></div>
<script>
  $("h1").click(function() {
    $(this)
      .parent()
      .css("background", "red");
  });
</script>
```

# 문서 객체 조작

## 문서 객체의 클래스 속성 추가

| 메서드     | 기능                         |
| ---------- | ---------------------------- |
| addClass() | 문서 객체의 클래스 속성 추가 |

복수의 객체가 선택될 때 일반적인 setter함수는 set 사항을 모두에게 적용시킴

```html
<h1>첫번째</h1>
<h1>두번째</h1>
<h1>세번째</h1>
<script>
  $("h1").addClass("item"); //다 적용됨
  //return type이 string인 함수를 매개변수로 사용할 수 있음
  $("h1").addClass(function(index) {
    return "class" + index;
  });
</script>
```

## 문서 객체의 클래스 속성 제거

| 메서드        | 기능                           |
| ------------- | ------------------------------ |
| removeClass() | 문서 객체의 클래스 속성을 제거 |

- 매개변수에 아무것도 입력하지 않을 시 모든 클래스 제거
- 매개변수에 입력 값이 있을시 입력된 클래스만 제거

## 문서 객체의 속성 검사(get)

| 메서드 | 기능                           |
| ------ | ------------------------------ |
| attr() | 속성과 관련된 모든 기능을 수행 |

대부분의 getter함수는 복수의 객체가 선택될 때 첫번째 한 개만 반환함

```html
<img src="1.jpg" />
<img src="2.jpg" />
<img src="3.jpg" />
<script>
  $("img").attr("src"); // "1.jpg" 반환
</script>
```

## 문서 객체의 속성 추가(set)

| 메서드 | 기능                           |
| ------ | ------------------------------ |
| attr() | 속성과 관련된 모든 기능을 수행 |

대부분의 setter함수는 복수의 객체가 선택될 때 모두에게 적용시킴

```html
<img src="1.jpg " /><img src="2.jpg" /><img src="3.jpg" />
<script>
  //다음 세 가지 형태로 사용가능
  $(selector).attr(name, value);

  //width를 100으로 통일
  $("img").attr("width", 100);
  $(selector).attr(name, function(index, attr) {});

  //width가 순서에 비례하여 커짐
  $("img").attr("width", function(index) {
    return (index + 1) * 100;
  });
  $(selector).attr(object);

  //2번에 1번을 살짝 혼합
  $("img").attr({
    height: 100,
    width: function(index) {
      return (index + 1) * 100;
    }
  });
</script>
```

## 문서 객체의 속성 제거(set)

| 메서드       | 기능                  |
| ------------ | --------------------- |
| removeAttr() | 문서 객체의 속성 제거 |

이것도 setter함수의 성격을 가짐

```html
<img src="1.jpg " /><img src="2.jpg" /><img src="3.jpg" />
<script>
  $("img").removeAttr("src"); //모든 src 다 삭제
</script>
```

## 문서 객체의 스타일 검사(get)

| 메서드 | 기능                             |
| ------ | -------------------------------- |
| css()  | 스타일과 관련된 모든 기능을 수행 |

대부분의 getter함수는 복수의 객체가 선택될 때 첫번째 한 개만 반환함

```javascript
$("h1").css("color"); //h1 객체들 중 첫번째 객체에 스타일 속성 중 'color' 속성의 값 반환
```

background-color처럼 -가 있으면 그대로 쓰거나 backgroundColor처럼 바꿈

## 문서 객체의 스타일 추가(set)

| 메서드 | 기능                             |
| ------ | -------------------------------- |
| css()  | 스타일과 관련된 모든 기능을 수행 |

- attr() 메서드 set버전과 사용법이 완벽히 똑같음
- 대부분의 setter함수는 복수의 객체가 선택될 때 모두에게 적용시킴

```html
<h1></h1>
<h1></h1>
<h1></h1>
<script>
  //다음 세 가지 형태로 사용가능
  $(selector).css(name, value);

  //color를 red로 통일
  $("h1").css("color", red);
  $(selector).css(name, function(index, attr) {});

  //color가 순서에 따라 바뀜
  color = ["red", "blue", "black"];
  $("h1").css("color", function(index) {
    return color[index];
  });
  $(selector).css(object);

  //2번을 object로 입력가능
  color = ["red", "blue", "black"];
  $("h1").css({
    backgroundColor: "orange",
    color: function(index) {
      return color[index];
    }
  });
</script>
```

## 문서 객체의 내부 검사(get)

| 메서드 | 기능                                                            |
| ------ | --------------------------------------------------------------- |
| html() | 문서 객체 내부의 글자와 관련된 모든 기능을 수행(HTML 태그 계산) |
| text() | 문서 객체 내부의 글자와 관련된 모든 기능을 수행                 |

매개변수가 없을시 getter 메서드 기능

```html
<h1>first</h1>
<h1>second</h1>
<h1>third</h1>
<script>
  $("h1").html(); //일반적인 getter 메서드처럼 first만 리턴
  $("h1").text(); //일반적인 getter 메서드와 달리 firstsecondthird 리턴
</script>
```

## 문서 객체의 내부 추가(set)

| 메서드 | 기능                                                            |
| ------ | --------------------------------------------------------------- |
| html() | 문서 객체 내부의 글자와 관련된 모든 기능을 수행(HTML 태그 계산) |
| text() | 문서 객체 내부의 글자와 관련된 모든 기능을 수행                 |

html() - 다음 두 가지 형태로 사용 가능

1. `$(selector).html(value)`
   태그 계산하여 value를 객체에 문자열로 입력
2. `$(selector).html(function(index,html){});`
   태그 계산하여 리턴값을 객체에 문자열로 입력

```html
<div></div>
<div></div>
<div></div>
<script>
  $("div").html(function(index) {
    return "<h1>" + (index + 1) + "번째</h1>"; //"n번째" 출력
  });
  //매개변수에 html이 있다면 기존에 입력된 값임
  $("h1").html(function(index, html) {
    return "★" + html + "★"; //"★n번째★" 출력
  });
</script>
```

text() - html()과 똑같은 2가지 방법으로 사용 가능
대신 HTML태그를 계산하지 않고 그대로 출력 ex) `<h1>1번째</h1>`

## 문서 객체 제거

| 메서드   | 기능                  |
| -------- | --------------------- |
| remove() | 문서 객체를 제거      |
| empty()  | 문서 객체 내부를 비움 |

## 문서 객체 생성1

| 메서드 | 기능             |
| ------ | ---------------- |
| \$()   | 문서 객체를 생성 |

```javascript
//())안에 'h1'처럼 괄호없이 쓰면 있는 태그 선택

//()안에 '<h1></h1>'처럼 괄호까지 쓰면 새로운 태그 생성
$("<h1></h1>");

//태그 생성 후 객체에 문자열 입력
$("<h1></h1>").html("태그 안에 문자열");

//문자열까지 입력된 태그를 body에 붙이기
$("<h1></h1>")
  .html("태그 안에 문자열")
  .appendTo("body");

//태그+문자열을 한번에 생성 후 body에 붙이기
$("<h1>태그 안에 문자열</h1>").appendTo("body");
```

## 문서 객체 생성2

| 메서드 | 기능             |
| ------ | ---------------- |
| \$()   | 문서 객체를 생성 |

```javascript
//태그 생성 후, 객체에 속성 입력 후, body에 붙이기
$("<img />")
  .attr("src", "apple.jpg")
  .appendTo("body");
//태그에 object로 (스타일)속성 부여하여 생성한 후, body에 붙이기
$("<img />", { src: "apple.jpg", width: "100px" }).appendTo("body");
```

## 문서 객체 삽입

| 메서드                | 기능                       |
| --------------------- | -------------------------- |
| \$(A).appendTo(B)     | A를 B안의 뒤쪽 부분에 추가 |
| \$(B).append(A)       | A를 B안의 뒤쪽 부분에 추가 |
| \$(A).prependTo(B)    | A를 B안의 앞쪽 부분에 추가 |
| \$(B).prepend(A)      | A를 B안의 앞쪽 부분에 추가 |
| \$(A).insertAfter(B)  | A를 B의 뒤에 추가          |
| \$(B).after(A)        | A를 B의 뒤에 추가          |
| \$(A).insertBefore(B) | A를 B의 앞에 추가          |
| \$(B).before(A)       | A를 B의 앞에 추가          |

8가지 메서드 사용법이 다 같으므로 append()메서드 하나만 코드 정리
다음 두 가지 형태로 사용 가능

```javascript
$(selector).append(content, content, ... , content)
//content에는 문자열 또는 jQuery 문서 객체가 들어갈 수 있음

var h1 = "<h1>큰 글씨</h1>";
var h2 = "<h2>작은 글씨</h2>";

//큰글씨, 작은글씨, 큰글씨, 작은글씨 순으로 출력
$('body').append(h1, h2, h1, h2);
$(selector).append(function(index){});
//매개함수는 문자열 또는 jQuery 문서 객체 반환
```

```html
<div></div>
<div></div>
<div></div>
<script>
  var content = [{}, {}, {}];
  $('div').append(function(index){
     				return content[index].~~ + content[index].~~ ;
  			   });
</script>
```

## 문서 객체 이동

이미지가 6개 있을때

```html
<body>
  <img src="1.jpg" />...<img src="6.jpg" />
</body>
<script>
  //body에 있던 객체들 중 맨 앞 객체를 body 맨 뒤로
  $("img")
    .first()
    .appendTo("body");
  //예쁜 슬라이드를 만들려면 width, height 통일하고 setInterval로 특정 시간마다
  $("img")
    .first()
    .appendTo("body");
</script>
```

## 문서 객체 복제

| 메서드  | 기능             |
| ------- | ---------------- |
| clone() | 문서 객체를 복제 |

문서 객체 삽입 메서드에서 A에 해당하는 객체가 이미 본문에 존재하는 객체라면
문서 객체 이동이 되는 것이고 이는 [Ctrl]+[X]나 마찬가지
이 경우, 기존 객체의 삭제를 원치 않는다면 기존객체.문서객체삽입메서드() 대신
기존객체.clone().문서객체삽입메서드() (기존객체를 복사하고 복사본을 삽입하기 때문에 기존객체 보존가능)

# 이벤트

## 기본 이벤트 연결

| 메서드 | 기능        |
| ------ | ----------- |
| on()   | 이벤트 연결 |

2가지 형태로 사용 가능

1. 매개변수 = 이벤트 이름, 이벤트 리스너

   ```javascript
   $(selector).on(eventName, function(event) {});
   $("h1").on("click", function() {
     $(this).html(function(index, html) {
       //이벤트 리스너안에서 this 키워드는 이벤트가 발생한 객체
       return html + "+";
     });
   });
   ```

2. 매개변수 = 객체(한번에 여러 이벤트 연결 가능)

   ```javascript
   $(selector).on(object);
   $("h1").on({
     mouseenter: function() {
       $(this).addClass("reverse");
     }, //클래스에 CSS를 지정해놓으면
     mouseleave: function() {
       \$(this).removeClass("reverse");
     } //이벤트에 효과를 줄 수 있음
   });
   ```

## 편한 이벤트 연결1

focus, focusout, scroll, click, mouseenter, mouseleave, keydown, keypress, ready 등등의 method

`$(selector).메서드(function(event){})`

보통 편한 연결을 사용하고, 기본 연결(on)을 사용해야 하는 경우도 있음

1. 한번에 여러 종류의 이벤트를 추가하는 건 기본 연결로 밖에 못함
2. 개발자가 직접 만든 이벤트나 표준에 아직 추가 안된 이벤트는 편한 연결에서 제공이 안됨

## 편한 이벤트 연결2

+++메서드+++ + hover() mouseenter 이벤트와 mouseleave 이벤트를 동시에 연결
++++++++++
2개의 이벤트를 연결하는 것이므로 매개변수로 이벤트리스너가 2개 필요함
$(selector).hover(function(event){},function(event){});
$('h1').hover({
function(){$(this).addClass('reverse')}, //mouseenter 효과
function(){$(this).removeClass('reverse')} //mouseleave 효과
});

## 이벤트 연결 제거

+++메서드+++ + off() 이벤트 제거
++++++++++
3가지 형태로 사용 가능 1. $(selector).off() //객체와 관련된 모든 이벤트 제거 2. $(selector).off(eventName) //객체의 특정 이벤트와 관련된 모든 이벤트 제거 3. \$(selector).off(eventName, function) //객체의 특정 이벤트 리스너 제거

## 일회성 이벤트 리스너

$('h1').on('click', function(){
$(this).html("Clicked, Listener disappeared");
\$(this).off();
});

## 일회성 이벤트 리스너

+++메서드+++ + one() 이벤트를 한번만 연결
++++++++++
on()과 사용법이 같고, 이벤트가 한번만 연결됨
매개변수 context
jQuery에는 매개변수가 사실 두 개이다. \$(selector, context)
selector : 선택자
context : selector가 적용하는 범위를 한정, 일반적으로 이벤트와 함께 사용
사용 예시 : 클릭된 div의 <h1>내용을 출력

<div><h1>first</h1></div>
<div><h1>second</h1></div>
<div><h1>third</h1></div>
$('div').click(function(){
var print = $('h1', this).text();
alert(print);
});
-> 그냥 $('h1').text() 하면 firstsecondthird 출력
find() 메서드를 활용해도 같은 결과를 낼 수 있다
$('div').click(function(){
var print = $(this).find('h1').text();
alert(print);
});

## 이벤트 객체

- 이벤트 발생 객체와는 다른 것으로, function(event)에서 매개변수로 쓰인 event를 의미함
- javascript의 이벤트 객체는 웹브라우저마다 사용법 및 속성이 다르나,
  jQuery의 이벤트 객체는 이들을 모두 정형화 해놓음. jQuery 공홈에서 확인 가능

| 속성                    | 기능                                                                             |
| ----------------------- | -------------------------------------------------------------------------------- |
| event.pageX             | 브라우저의 화면을 기준으로 한 마우스의 X 좌표 위치 //canvas 태그와 연계하여 쓰임 |
| event.pageY             | 브라우저의 화면을 기준으로 한 마우스의 Y 좌표 위치                               |
| event.preventDefault()  | 기본 이벤트를 제거                                                               |
| event.stopPropagation() | 이벤트 전달을 제거                                                               |

## 이벤트 강제 발생

| 메서드    | 기능                     |
| --------- | ------------------------ |
| trigger() | 이벤트를 강제로 발생시킴 |

2가지 형태로 사용

1. \$(selector).trigger(eventName)
2. \$(selector).trigger(eventName, data) //data는 배열임

**EX : 1초마다 이벤트 강제 발생**

```html
<h1>Start:</h1>
<h1>Start:</h1>
<script>
  //모든 h1태그는 클릭시마다 ★한개 추가
  $("h1").click(function() {
    $(this).html(function(index, html) {
      return html + "★";
    });
  });

  //마지막 h1태그는 1초마다 클릭한것처럼 이벤트강제실행(★한개 자동 추가)
  setInterval(function() {
    $("h1")
      .last()
      .trigger("click");
  }, 1000);

  //간단한 연결방식이 사용가능한 이벤트는 다음과 같이 강제실행 가능
  setInterval(function() {
    $("h1")
      .last()
      .click();
  }, 1000);

  //하지만 간단한 연결방식이 사용불가능한 경우도 많으므로 가급적 trigger() 메서드사용;
</script>
```

**EX : trigger()메서드로 매개변수 전달하기**

```javascript
$("h1").click(function(event, data1, data2) {
  alert(data1 + " : " + data2);
});
$("h1")
  .eq(1)
  .trigger("click", [7, 9]); //매개변수들을 배열로 입력
```

## 기본 이벤트와 이벤트 전달

| 메서드            | 기능               |
| ----------------- | ------------------ |
| preventDefualt()  | 기본 이벤트를 제거 |
| stopPropagation() | 이벤트 전달을 제거 |

**EX : 하이퍼링크 기능 제거**

```html
<h1><a href="https://www.naver.com">★링크</a></h1>
-> "★링크"를 클릭하면 페이지가 이동하여 h1 태그의 이벤트가 기능을 하지 못하게
된다. -> 고로 a태그의 기본 이벤트를 제거
<style>
  \* {
    margin: 5px;
    padding: 5px;
    border: 3px solid black;
  }
</style>
<script>
  $("a").click(function(event) {
    $(this).css("background-color", "blue");
    event.preventDefault();
  });
  $("h1").click(function() {
    $(this).css("background-color", "red");
  });
</script>
```

**EX : 하이퍼링크 기능 제거 & h1 태그로의 이벤트 전달 제거**

```javascript
$("a").click(function(event) {
  $(this).css("background-color", "blue");
  event.stopPropagation(); //+1
  event.preventDefault(); //+2
});
```

-> +1, +2 를 한번에 return false;로 적을 수 있음
-> (주의) javascript에서 return false;는 기본 이벤트만 제거한다는 점에서 다름

## 이벤트 연결 범위 한정

on() 메서드에는 사실 eventName, eventListener 외 여러가지 매개변수가 있다.
그 중에 selector 매개변수는 이벤트의 범위를 한정시킨다 : delegate방식

**EX : selector 매개변수 사용X**

```html
<div id="wrap"><h1>원본</h1></div>
<script>
  $("h1").on("click", function() {
    var length = $("h1").length; //h1 객체의 개수
    var targetHTML = $(this).html(); //"원본" 가져옴
    $("#wrap").append("<h1>" + length + "-" + targetHTML + "</h1>");
  });
</script>
```

-> "원본" 클릭시마다 1-원본, 2-원본, ... 등 h1태그가 하나씩 새로이 생성됨
-> 다만, 숫자가 붙은 h1태그들은 h1태그지만 클릭해도 새로운 HEADER를 생성하지 못함
-> 처음의 on()메서드가 그 당시 존재하는 태그에만 이벤트를 연결했기 때문임
-> 그래서 상위 태그에 이벤트를 연결해두고 'h1 태그를 클릭했을때'를 검출해야함

**EX : selector 매개변수 사용**

```javascript
$("#wrap").on("click", "h1", function() {
  //이벤트를 상위 태그에 연결함
  var length = $("h1").length; //h1 객체의 개수
  var targetHTML = $(this).html(); //this = 클릭된 h1태그
  $("#wrap").append("<h1>" + length + "-" + targetHTML + "</h1>");
});
```

-> "원본" 클릭시마다 1-원본, 2-원본, ... 등 h1태그가 하나씩 새로이 생성됨
-> 신생 h1태그 클릭 시 "n-n-,,,-n-원본"의 새로운 h1태그가 생성됨

상위 개념이 애매한 태그는 document 객체에 이벤트를 연결해도 됨

```javascript
$(document).on("click", "h1", function() {});
```

delegate 방식으로 연결한 on() 메서드의 이벤트 리스너 삭제

```javscript
$('#wrap').off('click', 'h1'); //마찬가지로 상위 태그 차원에서 삭제
```

## 마우스 이벤트

| 메서드     | 기능                                                |
| ---------- | --------------------------------------------------- |
| click      | 마우스를 클릭할 때 발생                             |
| dbclick    | 마우스를 더블 클릭할 때 발생                        |
| mousedown  | 마우스 버튼을 누를 때 발생                          |
| mouseup    | 마우스 버튼을 뗄 때 발생                            |
| mouseenter | 마우스가 요소의 경계 외부에서 내부로 이동할 때 발생 |
| mouseleave | 마우스가 요소의 경계 내부에서 외부로 이동할 때 발생 |
| mousemove  | 마우스를 움직일 때 발생                             |
| mouseout   | 마우스가 요소를 벗어날 때 발생                      |
| mouseover  | 마우스가 요소 안에 들어올때 발생                    |

mouseover 이벤트와 mouseenter 이벤트의 차이
(mouseover는 거의 안 쓰이고 mouseenter가 많이 쓰임)

`+ 멘틀 + 외핵 + 내핵 + 외핵 + 멘틀 +`

- mouseover : 멘틀->외핵, 내핵->외핵, ...등 //외내부 순서 상관없이 특정 요소 안에 들어올 때
- mouseenter : 멘틀->외핵, 외핵->내핵 //외부에서 내부로 이동할 때 발생

## 키보드 이벤트

| 메서드   | 기능                  |
| -------- | --------------------- |
| keydown  | 키보드 누를 때 발생   |
| keypress | 글자가 입력될 때 발생 |
| keyup    | 키보드를 뗄 때 발생   |

글자수 세기 소스

1. textarea태그에 keyup이벤트를 연결
2. 한글은 keypress이벤트를 지원하지 않아서 keyup을 써야함
3. 이 방법은 다만 계속 누르고 있는 경우에는 쓸 수 없음

```html
<h1>150</h1>
<textarea></textarea>
<script>
  $("textarea").keyup(function() {
    var inputLength = $(this).val().length;
    var remain = 150 - inputLength;
    $("h1").html(remain);
  });
  //키보드 누를 때 이벤트 발생 순서
  //키보드 누름 -> "keydown" -> 글자가 입력됨 -> "keypress" -> 키보드에서 손을 뗌 -> "keyup"
</script>
```

## 윈도우 이벤트

윈도우 이벤트는 윈도우 객체 뿐 아니라 window객체와 document객체 이외에 img 태그 등이 사용할 수 있는 이벤트

| 메서드 | 기능                                |
| ------ | ----------------------------------- |
| ready  | 문서 객체가 준비 완료되면 발생      |
| load   | 문서 객체를 불러들일 때 발생        |
| unload | 문서 객체를 닫을 때 발생            |
| resize | 문서 객체의 크기를 변화시킬 때 발생 |
| scroll | 문서 객체를 스크롤할 때 발생        |
| error  | 에러가 있을 때 발생                 |

무한 스크롤 예제 소스

```javascript
$(window).scroll(function() {
  //한번만 굴려도 스크롤 이벤트 발생
  var scrollHeight = $(window).scrollTop() + $(window).height(); //지금까지 스크롤한 길이 + 보이는 화면의 높이
  var documentHeight = \$(document).height(); //문서 전체의 높이

  if (scrollHeight == documentHeight) {
    //문서 전체의 끝이 보인다면
    for (var i = 0; i < 10; i++) {
      \$("<h1>INFINITY STONE</h1>").appendTo("body");
    }
  }
});
```

## 입력 양식 이벤트

| 메서드   | 기능                                                                    |
| -------- | ----------------------------------------------------------------------- |
| change   | 입력 양식의 내용을 변경할 때 발생                                       |
| focus    | 입력 양식의 초점을 맞추면 발생                                          |
| focusin  | 입력 양식에 초점이 맞추어지기 바로 전에 발생                            |
| focusout | 입력 양식에 초점이 사라지기 바로 전에 발생                              |
| blur     | 입력 양식에 초점이 사라지면 발생                                        |
| select   | 입력 양식을 선택할 때 발생(type=text 인 input태그 및 textarea태그 제외) |
| submit   | submit 버튼을 누르면 발생                                               |
| reset    | reset 버튼을 누르면 발생                                                |

```html
<form id="form">
  <div id="check">
    <input type="checkbox" />
    <input type="checkbox" />
    <input type="checkbox" />
  </div>
  <input type="submit" />
</form>
<script>
  //submit 기본 이벤트 제거
  $("#form").submit(function(event) {
    //submit은 input태그의 type값이지만 form태그의 이벤트임
    alert("제출안하고 이 메세지 출력");
    event.preventDefault(); //기본 이벤트를 제거
  });
  //하나 체크되면 나머지 다 자동 체크
  $("#check").change(function() {
    //type값이 checkbox와 radio인 input태그는 상태 변경 이벤트가 click이 아니고 change임
    if (this.checked) {
      //checked 속성 : 입력 객체의 체크 상태 확인
      $("#check")
        .children()
        .prop("checked", true); //prop 메서드 : 체크 상태를 바꿈
    } else {
      $("#check")
        .children()
        .prop("checked", false);
    }
  });
</script>
```

# 효과

## 기본 시각 효과

| 메서드        | 기능                                            |
| ------------- | ----------------------------------------------- |
| show()        | 문서 객체를 크게 확대하며 보여줌                |
| hide()        | 문서 객체를 작게 축소하며 사라지게 함           |
| toggle()      | show()메서드와 hide()메서드를 번갈아 실행       |
| slideDown()   | 문서 객체를 슬라이드 효과와 함께 보여줌         |
| slideUp()     | 문서 객체를 슬라이드 효과와 함께 사라지게 함    |
| slideToggle() | slideDown()메서드와 slideUp메서드를 번갈아 실행 |
| fadeIn()      | 문서 객체를 선명하게 보여줌                     |
| fadeOut()     | 문서 객체를 흐리게 사라지게 함                  |
| fadeToggle()  | fadeIn()메서드와 fadeOut()메서드를 번갈아 실행  |

메서드 사용 형태

1.  \$(selector).method();
2.  \$(selector).method(speed);
3.  \$(selector).method(speed, callback);
4.  \$(selector).method(speed, easing, callback);

각 매개변수의 의미

- speed - 효과를 진행할 속도를 지정, 밀리초 단위의 숫자 또는 slow, normal, fast 입력
- callback - 효과를 모두 완료하고 실행할 함수
- easing - 애니메이션의 easing 형태를 지정, 플러그인이 없으면 linear 또는 swing 입력

## 사용자 정의 효과

| 메서드    | 기능                    |
| --------- | ----------------------- |
| animate() | 사용자 지정 효과를 생성 |

메서드 사용 형태

1. \$(selector).animate(object);
2. \$(selector).animate(object, speed);
3. \$(selector).animate(object, speed, easing);
4. \$(selector).animate(object, speed, easing, callback);

각 매개변수의 의미

- speed, callback, easing - 기본 시각 효과의 메서드와 동일
- object - 객체이고, 현재 상태에서 이 객체에 정의한 형태로 애니메이션이 동작함

object 객체의 속성

- opacity, height, top, width, margin, right, padding, bottom
- 위치 속성(heigh, top)을 변경하려면 객체의 position스타일 속성이 absolute나 relative로 지정되어있어야 함

사각형을 좌우로 움직이는 소스

```html
<div></div>
<div></div>
<div></div>
<div></div>
<style>
  div {
    width: 50px;
    height: 50px;
    background-color: orange;
    position: relative; //left속성을 변경할 것이므로 position 스타일 속성을 지정해둠
  }
</style>
<script>
  $("div").hover(
    function() {
      $(this).animate({ left: 500 }, "slow");
    },
    function() {
      \$(this).animate({ left: 500 }, "slow");
    }
  );
</script>
```

> 윤인성 선생님의 Javascript 저서를 참고했습니다.
