---
title: 개발 - Markdown
date: 2020-07-05 16:11:50
tags:
  - markdown
category:
  - 개발
  - markdown
---

# 표준 문법

## Headings

```
# h1 Heading
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
```

# h1 Heading

## h2 Heading

### h3 Heading

#### h4 Heading

##### h5 Heading

###### h6 Heading

## Paragraphs

그냥 평범하게 쓰면 문단으로써 들어감

```
Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri, animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex, soluta officiis concludaturque ei qui, vide sensibus vim ad.
```

Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri, animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex, soluta officiis concludaturque ei qui, vide sensibus vim ad.

## Breaks

"\n" 이나 `<br>` 같은 문법이 없으므로 아래와 같이 `<hr>`선을 그어주는 방식으로 사용

- `___`, `---`, `***`

---

## Emphasis

### Bold

```
**굵은 글씨 표기**
```

**굵은 글씨 표기**

### Italics

```
_이탈리안 표기_
```

_이탈리안 표기_

## Blockquotes

Blockquotes(인용)을 하려면 `>` 사용

```
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante
```

> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.

## Lists

### Unordered

\*, -, + 모두 같음

```
* valid bullet
- valid bullet
+ valid bullet
```

For example

```
+ Lorem ipsum dolor sit amet
+ Consectetur adipiscing elit
+ Integer molestie lorem at massa
+ Facilisis in pretium nisl aliquet
+ Nulla volutpat aliquam velit
  - Phasellus iaculis neque
  - Purus sodales ultricies
  - Vestibulum laoreet porttitor sem
  - Ac tristique libero volutpat at
+ Faucibus porta lacus fringilla vel
+ Aenean sit amet erat nunc
+ Eget porttitor lorem
```

Renders to:

- Lorem ipsum dolor sit amet
- Consectetur adipiscing elit
- Integer molestie lorem at massa
- Facilisis in pretium nisl aliquet
- Nulla volutpat aliquam velit
  - Phasellus iaculis neque
  - Purus sodales ultricies
  - Vestibulum laoreet porttitor sem
  - Ac tristique libero volutpat at
- Faucibus porta lacus fringilla vel
- Aenean sit amet erat nunc
- Eget porttitor lorem

### Ordered

A list of items in which the order of items does explicitly matter.

```
1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis in pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Aenean sit amet erat nunc
8. Eget porttitor lorem
```

Renders to:

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis in pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Aenean sit amet erat nunc
8. Eget porttitor lorem

## Code

### Inline code

backtick <code>`</code> 으로 원하는 부분을 감싸면 됨

`# 굵은 글자` inline with other text, just wrap it in backticks.

### Fenced code block

backtick 3개 <code>```</code>로 감싸면 "code fences"라고 부름
(말 만들기 참 좋아함)

<pre>
```
# 이렇게 마크다운 형식으로 작성하든
<div>html로 작성하든</div>
text로써 읽힘
```
</pre>

### Syntax highlighting

원하는 언어를 붙여 <code>```js</code> 와 같이 작성

<pre>
```js
const name = "kyh";
console.log(name);
```
</pre>

```js
const name = "kyh";
console.log(name);
```

## Links

### Autolinks

```
<https://newtype94.github.io>
```

<https://newtype94.github.io>

### Inline links

```
[Blog](http://newtype94.github.io)
```

[Blog](http://newtype94.github.io)

### Link titles

```
[Blog](http://newtype94.github.io "It is my blog..")
```

[Blog](http://newtype94.github.io "It is my blog..")

### Named Anchors

markdown 페이지 내에서 서로 이동할 수 있는 일종의 Anchor

```
# Table of Contents
  * [Chapter 1](#chapter-1)
  * [Chapter 2](#chapter-2)
  * [Chapter 3](#chapter-3)
```

```
## Chapter 1 <a name="chapter-1"></a>
Content for chapter one.

## Chapter 2 <a name="chapter-2"></a>
Content for chapter one.

## Chapter 3 <a name="chapter-3"></a>
Content for chapter one.
```

## Images

```
![고양이](/image/고양이.jpg)
```

![고양이](/image/고양이.jpg)

또는

```
![고양이](/image/고양이.jpg "고양이 사진입니다")
```

![고양이](/image/고양이.jpg "고양이 사진입니다")

또는

```
![고양이][id]
```

![고양이][id]

그리고 id에 사진의 링크 정의하여 후술해야함

[id]: /image/고양이.jpg "고양이 링크"

```
[id]: /image/고양이.jpg "고양이 링크"
```

## Raw HTML

`<` 와 `>`를 사용하면 자동으로 html의 태그로 인식됨

```
**제 깃으로 놀러오세요 <a href="https://github.com/newtype94">newtype94</a>.**
```

**제 깃으로 놀러오세요 <a href="https://github.com/newtype94">newtype94</a>.**

## backslash 표현

markdown 문법에 사용되는 특수 문자를 따로 표시하고 싶을 때

```
\*this is not italic*
```

\*this is not italic\*

# 비표준 문법 (Github, Gitlab 전용)

## Strikethrough

```
~~Strike through this text.~~
```

~~Strike through this text.~~

### Todo List

```
- [ ] Lorem ipsum dolor sit amet
- [ ] Consectetur adipiscing elit
- [ ] Integer molestie lorem at massa
```

- [ ] Lorem ipsum dolor sit amet
- [ ] Consectetur adipiscing elit
- [ ] Integer molestie lorem at massa

**Links in todo lists**

```
- [ ] [foo](#bar)
- [ ] [baz](#qux)
- [ ] [fez](#faz)
```

- [ ] [foo](#bar)
- [ ] [baz](#qux)
- [ ] [fez](#faz)

## Tables

```
| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
```

| Option | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default.    |
| ext    | extension to be used for dest files.                                      |

### Aligning cells

**가운데 정렬**

```
| Option | Description |
| -:- | -:- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
```

**오른쪽 정렬**

```
| Option | Description |
| ------:| -----------:|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
```
