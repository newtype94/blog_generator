---
title: 카카오 blind 2019 징검다리 건너기
date: 2020-07-30 11:23:14
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2019 인턴
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64062)

# 문제 풀이

완전 탐색으로 풀면 시간초과가 발생한다.
최악의 경우
stones의 최대 length(200,000) x stones 원소의 최댓값(200,000,000)
만큼의 탐색이 필요하기 때문에..

이 때 stones의 최대 length는 건너뛰지 못해도
stones의 각 값에는 이분탐색을 적용할 수 있다.

내 차례가 다가왔다. (앞에 n명이 건넜다)
내가 마주보든 stones는 초기 stones의 모든 값에 n을 뺀것과 같다.
stones에는 0 이하의 수, 0 초과의 수가 존재할 것이다.
0이하의 수가 연속되는 길이가 k를 넘지 않으면
나도 건널 수 있다.

이 n은 앞서 말한 stones 원소의 최댓값(200,000,000)까지 가능하므로
이분탐색을 도입!

# 전체 코드

```javascript
function solution(stones, k) {
  let left = 0;
  let right = 200000000;

  while (1) {
    if (right - left === 1) return left;
    const mid = Math.floor((left + right) / 2);
    zeroSucceed(mid) ? (left = mid) : (right = mid);
  }

  function zeroSucceed(n) {
    let succeed = 0;
    for (let v of stones) {
      if (v - (n - 1) <= 0) {
        succeed++;
        if (succeed >= k) return false;
      } else succeed = 0;
    }
    return true;
  }
}
```
