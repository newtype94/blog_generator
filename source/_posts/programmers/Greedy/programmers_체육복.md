---
title: programmers 체육복
date: 2020-02-09 17:21:30
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.1 / Javscript

# 설명

평범하게 한번만 루프를 돌면 될 것 같은 문제인데,
문제에서 여분을 가져온 사람이 도난을 당하면 그 경우를 최우선으로 처리한다고 명시해놓았다.
그래서 루프를 2번 돌아야한다.

1. lost와 reserve에서 같은 요소가 있다면 둘 다 빼는 루프
2. lost 요소 - 1 == reserve 요소
   or
   lost 요소 + 1 == reserve 요소
   인 경우, lost와 reserve에서 각 요소 제거

# 전체 코드

```javascript
function solution(n, lost, reserve) {
  lost = lost.reduce((acc, cur) => {
    const a = reserve.indexOf(cur);
    if (a > -1) {
      reserve.splice(a, 1);
      return acc;
    }
    acc.push(cur);
    return acc;
  }, []);

  lost = lost.reduce((acc, cur) => {
    const a = reserve.indexOf(cur - 1);
    if (a > -1) {
      reserve.splice(a, 1);
      return acc;
    }
    const b = reserve.indexOf(cur + 1);
    if (b > -1) {
      reserve.splice(b, 1);
      return acc;
    }
    acc.push(cur);
    return acc;
  }, []);

  return n - lost.length;
}
```
