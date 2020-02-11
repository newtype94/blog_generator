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

# 분류 / 레벨 / 언어

완전탐색 / LV.2 / Javscript

# 설명

소수를 찾는 문제인데 크게 구현해줄 함수가 2개 있다.

1. number => 소수여부 // return type = boolean
2. string => [숫자들의 배열] // return type = array

이 함수들을 main함수 밖에서 정의하고
2번 함수 결과(Array)의 모든 요소에 1번 함수를 적용시킨 후
거기서 true인 것의 개수를 반환하면 그것이 답이다!

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

const sumLists = numlists => {
  let lists = new Set();

  const makeSum = (sum, remains, cnt) => {
    if (cnt > 0)
      remains.forEach((remain, i) => {
        let remainsCopy = remains.slice(0, remains.length);
        remainsCopy.splice(i, 1);
        makeSum(sum + remain * Math.pow(10, cnt - 1), remainsCopy, cnt - 1);
      });
    else {
      lists.add(sum);
    }
  };

  for (let i = 1; i <= numlists.length; i++) {
    makeSum(0, numlists, i);
  }

  return Array.from(lists);
};

function solution(numbers) {
  return sumLists(numbers.split("").map(string => parseInt(string))).filter(n =>
    isSoSu(n)
  ).length;
}
```
