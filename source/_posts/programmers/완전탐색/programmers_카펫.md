---
title: programmers 카펫
date: 2020-02-21 11:54:17
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

대기업 인적성에 규칙 찾기 part로 나오는 유형과 비슷하다.
이 문제에서는 brown 블록과 red 블록의 규칙을 찾는게 우선이다.

1. 전체 블록은 "가로 >= 세로"
2. red 블록은 내키는대로 존재하고 brown은 그것을 1겹으로 둘러싸고 있음.

for문, while문, 재귀 중 아무거나 사용하여 완전탐색을 하면 되고,
나는 for문을 사용하는 대신, 전체 블록의 루트를 for문의 끝으로 지정했다.

# 전체 코드

```javascript
function solution(brown, red) {
  const big = brown + red;
  let max = Math.floor(Math.sqrt(big));

  for (let i = 3; i < max + 1; i++) {
    if (big % i === 0 && (big / i - 2) * (i - 2) === red) return [big / i, i];
  }
}
```
