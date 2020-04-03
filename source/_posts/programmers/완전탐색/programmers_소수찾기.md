---
title: programmers 소수 찾기
date: 2020-02-10 15:17:50
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 완전탐색
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42839)

# 분류 / 레벨 / 언어

완전탐색 / LV.2 / Javscript

# 설명

소수를 찾는 문제인데 크게 구현해줄 함수가 2개 있다.

1. number => 소수여부: boolean
2. string => [숫자들의 배열]: array

이 함수들을 따로 정의하고
1번 함수 ( 2번 함수 (문제 input) ) 의 return 값 중
true인 것의 개수를 반환하면 답이다.

# 전체 코드

```javascript
const isSoSu = n => {
  if (n === 0 || n === 1) return false;
  if (n === 2 || n === 3) return true;
  for (let i = 2; i <= n / 2; i++) {
    if (n % i === 0) return false;
  }
  return true;
};

const makeNum = numList => {
  const numSet = new Set();

  const makeSum = (sum, remains, cnt) => {
    if (cnt > 0)
      for (let i = 0; i < remains.length; i++) {
        const copy = remains.slice();
        makeSum(sum + copy.splice(i, 1) * Math.pow(10, cnt - 1), copy, cnt - 1);
      }
    else numSet.add(sum);
  };

  for (let i = 1; i <= numList.length; i++) {
    makeSum(0, numList, i);
  }

  return [...numSet];
};

function solution(numbers) {
  return makeNum(numbers.split("").map(v => 0 + v)).filter(n => isSoSu(n))
    .length;
}
```
