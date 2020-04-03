---
title: programmers 기능개발
date: 2020-02-08 14:21:32
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 스택, 큐
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42586)

# 분류 / 레벨 / 언어

스택,큐 / LV.2 / Javscript

# 설명

어떤 것을 만들어서 => 어떤 순서로 => 어떤 기준으로
처리할지만 생각하면 된다.
배열과 조건문만 알아도 풀 수 있다.

JS array의 내장함수 map과 reduce를 사용!

# 전체 코드

```javascript
let days = 0;

function solution(progresses, speeds) {
  return progresses
    .map((progress, i) => Math.ceil((100 - progress) / speeds[i]))
    .reduce((acc, curr) => {
      if (curr > days) {
        days = curr;
        acc.push(1);
      } else acc[acc.length - 1] += 1;
      return acc;
    }, []);
}
```
