---
title: 카카오 blind 2018 방금그곡
date: 2020-04-10 14:01:14
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17683)

# 문제 풀이

구현의 성격이 강하다.
단 문제의 조건을 놓치지 않고 필요한 함수를 정의해야한다.

문제의 C#, D# 같이 #이 붙는 경우 문자열은 2개이지만 1개로 계산해야하므로
소문자 c, 소문자 d등으로 대체했다.

# 전체 코드

```javascript
const converter = (input) =>
  input
    .split("")
    .reduce(
      (acc, cur) =>
        cur === "#" ? acc.concat(acc.pop().toLowerCase()) : acc.concat(cur),
      []
    )
    .join("");

const timer = (start, end) =>
  parseInt(end.slice(0, 2)) * 60 -
  parseInt(start.slice(0, 2)) * 60 +
  parseInt(end.slice(3, 5)) -
  parseInt(start.slice(3, 5));

function solution(m, musicinfos) {
  m = converter(m);

  musicinfos = musicinfos
    .map((v) => (v = v.split(",")))
    .map((v) => [timer(v[0], v[1]), v[2], converter(v[3])])
    .sort((a, b) => b[0] - a[0]);

  for (let v of musicinfos) {
    let temp = "";
    for (let i = 1; i <= v[0] / v[2].length; i++) {
      temp += v[2];
    }
    temp += v[2].slice(0, v[0] % v[2].length);
    if (temp.indexOf(m) > -1) return v[1];
  }
  return "(None)";
}
```
