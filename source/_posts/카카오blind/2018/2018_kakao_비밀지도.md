---
title: 카카오 blind 2018 비밀지도
date: 2020-10-07 12:11:46
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17681)

# 문제 풀이

각 언어 별 숫자-문자열 변환 방식을 알고 있어야한다.
진수 변환까지 알고 있으면 좋다.

# 전체 코드

```javascript
function solution(n, arr1, arr2) {
  const numToString = (num) => {
    let a1 = num.toString(2);
    while (a1.length < n) {
      a1 = "0" + a1;
    }
    return a1;
  };

  arr1 = arr1.map(numToString);
  arr2 = arr2.map(numToString);

  const answer = [];

  for (let a = 0; a < n; a++) {
    const temp = [];
    for (let b = 0; b < n; b++) {
      if (arr1[a][b] === "0" && arr2[a][b] === "0") temp.push(" ");
      else temp.push("#");
    }
    answer.push(temp.join(""));
  }

  return answer;
}
```
