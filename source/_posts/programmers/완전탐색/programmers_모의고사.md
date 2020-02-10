---
title: programmers 모의고사
date: 2020-02-10 13:26:50
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스
  - 완전탐색
---

# 분류 / 레벨 / 언어

완전탐색 / LV.1 / Javscript

# 설명

완전탐색은 사실상 대기업 코딩테스트에서 가장 많이 나오는 주제이다.
별도의 방법론이 필요없고, 모든 경우의 수를 검증해주도록 코딩만 하면 된다.
그래서 알고리즘 트레이닝을 안 하고 서비스 개발만 주로 했던 학부생(나)도 부담없이 풀 수 있다.

# 전체 코드

```javascript
const picks = [
  [1, 2, 3, 4, 5],
  [2, 1, 2, 3, 2, 4, 2, 5],
  [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]
];
const pickCycles = [5, 8, 10];

function solution(answers) {
  return answers
    .reduce(
      (acc, curr, currIdx) => {
        pickCycles.forEach((cycle, i) => {
          if (picks[i][currIdx % cycle] === curr) acc[i] += 1;
        });
        return acc;
      },
      [0, 0, 0]
    )
    .reduce(
      (acc, curr, currIdx) => {
        if (curr > acc.max) {
          acc.list = [currIdx + 1];
          acc.max = curr;
        } else if (curr === acc.max) acc.list.push(currIdx + 1);
        return acc;
      },
      { list: [], max: 0 }
    ).list;
}
```
