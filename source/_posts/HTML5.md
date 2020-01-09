---
title: HTML5
date: 2017-02-10 17:11:14
tags:
  - html5
category:
  - web
  - html5
---

> 윤인성 선생님의 HTML5 저서를 참고했습니다.

## script, link

```
<head>
	<link rel="stylesheet" href="경로"/>
	<script src="경로"></script>
</head>
```

## 특수 문자

`&nbsp;` 공백
`&lt;` <
`&gt;` >
`&amp;` &

## 기본 태그

`<br>` 개행
`<hr>` 수평 줄
`<a href="경로"></a>`
절대경로, 상대경로, 아이디경로(#id), 메일경로(mailto : 주소)

`<h1>~<h6>` 크기
`<p>` 문단
`<b>`굵은글자 `<i>`기울어진 글자 `<small>`작은 글자
`<sub>`아래 첨자 `<sup>`위 첨자 `<ins>`밑줄 `<del>`취소선

`<ul><li></li><li></li></ul>` 기호 목록
`<ol><li></li><li></li></ol>` 기호 목록

`<img src="경로" alt="이미지없을때 멘트" width="너비" height="높이">`

## 테이블

`<table>`, `<table border="1">`
(`<thead>` `<tbody>` `<tfoot>`)
`<tr>`//개행
`<th>`//제목 `<th colspan="2">`//제목,너비2
`<td>`//요소 `<td rowspan="4">`//요소,줄4

## div, span

`<div>` 블록 형식으로 공간분할, 한 행을 다 차지
`<span>` 인라인 형식으로 공간분할, 컨텐츠 크기만큼 차지

## 블록형식

`<div>`, `<h1>`~`<h6>`, `<p>`, 목록태그, 테이블태그, 입력양식태그

## 인라인 형식

`<span>`, `<a>`, `<input>`, 글자형식태그

## 시맨틱태그

`<header>`, `<nav>`, `<aside>`, `<section>`, `<article>`, `<footer>`

## 오디오태그

```html
<audio src="경로" preload autoplay loop controls></audio>
```

1.  preload - 재생전에 로딩완료 여부, autoplay - 자동재생여부, loop - 반복여부, controls - 재생도구 출력여부
2.  4가지 속성을 loop="loop"처럼 xhtml5형식으로 해도 됨

```html
//브라우저 제약 없는 오디오태그
<audio controls="controls">
  <source src="ka.mp3" type="audio/mp3" />
  <source src="ka.ogg" type="audio/ogg" />
</audio>
```

## 비디오태그

```html
<video
  src="경로"
  poster="경로"
  preload
  autoplay
  loop
  controls
  width="1"
  height="1"
></video>

//브라우저 제약 없는 비디오태그
<video controls="controls">
  <source src="wi.mp4" type="video/mp4" />
  <source src="wi.webm" type="video/mp4" />
</video>
```

## form 태그

```html
<form action="전송위치(목적지)" method="get||post">
  //"get" -> 데이터가 url에 들어감, "post" -> 데이터가 body에 담겨 전송됨
</form>
```

## input(입력양식) 태그

`<input type="">` 속성(type)이 성격을 결정함

1. 직접 입력하는 타입
   `<input type="text" name="액션페이지로 전달매개" value="전달값(디폴트값)" />`
   | type | 기능 |
   | -------- | ------------------- |
   | text | 텍스트상자 |
   | password | 암호화된 텍스트상자 |
   | file | 파일선택버튼 |
   | checkbox | 체크박스 |
   | radio | 라디오버튼 |

2. 버튼을 누르는 타입
   `<input type="button" value="버튼이름" />`
   | type | 기능 |
   | -------- | ------------------- |
   |button | 버튼
   |reset | 리셋버튼
   |submit | 제출버튼
   |image | 이미지

3. 안 보이는 타입
   `<input type="hidden" name="hidden" value="hidden" />`
   | type | 기능 |
   | -------- | ------------------- |
   | hidden | 안보임

## input태그에 라벨 붙이기

```html
<label for="name">라벨지</label> <input id="name" type="text" />
```

## textarea 태그

```html
<textarea cols="너비" row="높이"></textarea>
```

## select 태그

```html
<select>
  = 하나만 선택
  <option>1</option>
  <option>2</option>
</select>

<select multiple="multiple">
  = 복수선택
  <option>1</option>
  <option>2</option>
</select>

<select>
  <optgroup label="Front">
    <option>HTML5</option>
    <option>CSS3</option>
    <option>Javascript</option>
  </optgroup>
  <optgroup label="Back">
    <option>PHP</option>
    <option>JSP</option>
  </optgroup>
</select>
```

## 입력양식 그룹으로 묶기

```html
<fieldset>
  <legend>입력양식</legend>
</fieldset>
```
