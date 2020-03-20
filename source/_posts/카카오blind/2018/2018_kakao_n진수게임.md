---
title: kakao n진수 게임
date: 2020-03-20 17:27:10
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

# 문제 풀이

구현의 성격이 강한 문제이다.
진수 변환하는 방법을 알고 있어야 빠르고 정확하게 풀 수 있다.
[진수 계산](https://newtype94.github.io/2020/02/12/ES6/%EC%A7%84%EC%88%98%20%EA%B3%84%EC%82%B0/)

# 전체 코드

```javascript
function solution(n, t, m, p) {
  let num = 0;
  let fullString = "";

  while (fullString.length < t * m) {
    fullString += num.toString(n).toUpperCase();
    num++;
  }

  return fullString
    .split("")
    .filter((v, i) => (i + 1 - p) % m === 0)
    .slice(0, t)
    .join("");
}
```
