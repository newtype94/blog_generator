---
title: 카카오 blind 2018 뉴스 클러스터링
date: 2020-09-09 09:25:35
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17677)

# 문제 풀이

배열과 문자열을 활용한 구현 문제이다.

# 전체 코드

```javascript
const words = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");

function solution(str1, str2) {
  str1 = str1.toUpperCase().split("");
  str2 = str2.toUpperCase().split("");

  const arr1 = [];
  const arr2 = [];

  for (let i = 0; i < str1.length - 1; i++) {
    if (!words.includes(str1[i]) || !words.includes(str1[i + 1])) continue;
    arr1.push(str1[i] + str1[i + 1]);
  }
  for (let i = 0; i < str2.length - 1; i++) {
    if (!words.includes(str2[i]) || !words.includes(str2[i + 1])) continue;
    arr2.push(str2[i] + str2[i + 1]);
  }

  arr1.sort();
  arr2.sort();

  let uset = [];
  const nset = [];

  for (let a of arr1) {
    const i = arr2.indexOf(a);
    if (i > -1) {
      arr2.splice(i, 1);
      nset.push(a);
    }
    uset.push(a);
  }

  uset = [...uset, ...arr2];

  return uset.length === 0
    ? 65536
    : Math.floor((65536 * nset.length) / uset.length);
}
```
