---
title: CSS3 속성
date: 2017-03-01 09:12:54
tags:
  - css3
category:
  - web
  - css3
---

## 크기 단위

| 단위 | 기준        | 설명                                          |
| ---- | ----------- | --------------------------------------------- |
| %    | 백분위 단위 | 기본으로 설정된 크기를 기준으로 상대적인 크기 |
| em   | 배수 단위   | 기본으로 설정된 크기를 기준으로 상대적인 크기 |
| px   | 픽셀        | 모니터의 전구 개수                            |

## 색상 단위

| 방식                          | 예시                           |
| ----------------------------- | ------------------------------ |
| rgb(red, green, blue)         | rgb(255, 255, 255)             |
| rgba(red, green, blue, alpha) | rgb(255, 255, 255, 0.5)        |
|                               | 0.0=완전투명 ~ 1.0=완전 불투명 |
| #000000                       | 0094FF                         |

## padding과 margin의 위치

= margin =
= border =
= padding =
= 글자 =
= padding =
= border =
= margin =

## 테두리

**border-width, border-style, border-color 속성을 모두 사용해야 테두리가 보임**
border : #, #, #으로 속성 3개 한큐에 가능

border-radius : px
border-radius : px, px, px, px
(1) (2)
(3) (4)

## display 속성

| 속성 값      | 기능                      |
| ------------ | ------------------------- |
| none         | 보이지않음                |
| block        | 블록형식으로 지정         |
| inline       | 인라인형식으로 지정       |
| inline-block | 인라인-블록 형식으로 지정 |

## 인라인 형식과 인라인-블록 형식

|             |                                            |
| ----------- | ------------------------------------------ |
| 인라인      | margin이 양옆으로만 차지                   |
| 인라인-블록 | 인라인이지만 margin이 양옆위아래로 다 차지 |

## 배경 속성

| 속성 이름             |                                                                              |
| --------------------- | ---------------------------------------------------------------------------- |
| background-image      | url('경로')                                                                  |
| background-image      | url('맨앞'), url('은'), url('왼쪽부터')                                      |
| background-size       | 너비 높이                                                                    |
| background-size       | 너비, 너비 -> 콤마가 들어가면 각각의 url에 너비로 적용됨.(특수한 상황에서만) |
| background-repeat     | (기본속성=repeat) no-repeat, repeat-x, repeat-y                              |
| background-attachment | fixed, scroll                                                                |
| background-position   | bottom, center, inherit, left, right, top, x축위치, x축위치 y축위치          |

## 글자 속성

| 속성        | 개요       | ex                                    | 특이사항                                      |
| ----------- | ---------- | ------------------------------------- | --------------------------------------------- |
| font-size   | 크기 단위  | smaller, small, medium, large, larger | (by default) p태그 = 16px, h1태그 = 32px      |
| font-family | 글자체이름 | '없는글꼴', Arial, 'Times New Roman'  | 여러개 입력할 경우 앞에서 부터 있는 걸로 적용 |
| font-style  |            | italic;                               |
| font-weight |            | bold;                                 |

## 하이퍼링크

```css
a {
  text-decoration: none;
} // 밑줄을 없애나 색상은 파란색 그대로
```

## position 속성

| 속성 값  | 기능                                |
| -------- | ----------------------------------- |
| static   | 상대 위치 좌표 설정                 |
| relative | 초기 위치에서 상하좌우로 이동       |
| absolute | 절대 위치 좌표 설정                 |
| fixed    | 화면을 기준으로 절대 위치 좌표 설정 |

## 위치 속성

화면의 테두리를 기준으로 얼만큼 떨어져있는지에 따라
left, top ,right, bottom 속성들을 쓴다.

## z-index

**시나리오**

1. 10x10 정사각형이 3개 있다.
2. left, top을 (1,1) (3,3) (5,5)로 설정하면 일부분이 중첩된다.
3. 별다른 처리를 안하면 나중에 나온 코드가 맨앞에 위치한다.
4. 999, 3456, 30 등 임의의 값을 z-index속성에 부여하여 위치를 조작한다. 값이 클수록 앞에 위치한다.

**고급 시나리오**

```html
<h1>프론트엔드</h1>
<div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
<h1>프론트엔드</h1>
```

1. box[div]태그에 absolute로 절대위치를 주면 부모[div]가 영역을 차지하지 못한다.
2. 심지어 다른 h1 글자들이 가려진다.
3. <해결책> 부모[div]에 높이를 준다. 그리고 position속성의 값을 relative로 한다.
4. <결과> 부모[div]는 형제 태그들과 무리없이 쌓이고, 자손[div]는 부모[div]의 위치를 기준으로 절대 좌표를 잡는다.

## overflow 속성

속성 값 : hidden // scroll

```css
overflow-x : scroll (가로로만 스크롤)
overflow-y : scroll (세로로만 스크롤)
```

## text-overflow

- 속성값 : ellipsis;
- 한 행을 넘어가는 글자는 ..으로 생략한다.

## float 속성

- 속성 값 : left // right
- 태그를 왼쪽부터 붙일지 오른쪽부터 붙일지 결정

## 수평 정렬 속성

- inline 속성 태그는 수평정렬에 의미가 없다
- block 속성 태그에서는
  text-align : center // left // right

## float으로 수평 정렬

1. 자손에게 float속성을 지정하고 부모의 overflow속성을 hidden으로 적용한다.
2. 부모에서 width속성과 height속성을 입력하지 않고 overflow속성을 적용하면 자손이 차지하는 너비를 모두 감싼다.
3. 이 방법이 싫다면 부모태그의 height속성을 지정하는 방법도 있다.
4. (감싸지 않는다면 float때문에 마냥 부유하기만 한다)

## 수직 정렬 속성

수직정렬 속성은 존재하지 않으나
다른 방법들이 있음(추후 정리 예정)

## body 전체를 중앙 정렬

```css
body {
  margin: 0 auto;
  width: 960px;
}
```

## 20px 정사각형 쌩 중앙 정렬

```css
box {
  position: absolute;
  left: 50%;
  right: 50%;
  margin-left: -10px;
  margin-right: -10px;
}
```

## 고정 네비바

```css
position: fixed;
```

> 윤인성 선생님의 CSS3 저서를 참고했습니다.
