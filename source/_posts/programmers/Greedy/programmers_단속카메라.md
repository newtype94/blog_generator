---
title: programmers 단속카메라
date: 2020-03-04 14:01:13
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42884)

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.3 / Javscript

# 설명

## 이분탐색 시도

차량의 대수가 1대 ~ 10000대 이다.
차량이 10000대 있을 때
운이 좋으면 카메라 1대로 끝나고, 운이 없으면 카메라를 10000대 두어야 한다.
return의 range가 넓기에 역으로 대입하고자 이분탐색의 틀을 먼저 짜보았다.

```javascript
function solution(routes) {
  routes.sort((a, b) => a[1] - b[1]).sort((a, b) => a[0] - b[0]);

  const setCam = () => {};

  let left = 1;
  let right = routes.length;
  let mid;

  while (right - left > 1) {
    mid = Math.floor((left + right) / 2);
    setCam(mid) ? (right = mid) : (left = mid);
  }

  return right;
}
```

setCam 함수를 greedy한 방법으로 구현하던 중,
그냥 setCam함수 자체가 바로 최솟값을 return할 수도 있겠다 싶었다.
그래서 이분탐색없이 푸는 것으로 방향을 바꿨다.

## 그리디 풀이

그리디 풀이는 부분의 답을 모아 최종 답이 도출하는 것이 원칙인데
이 때 "부분"을 어떤 것으로 잡는지가 중요하다.
사람의 직관으로는 먼저 출발하는 차를 우선적으로 고려하고 전체의 답을 향해 더해나갈 것이지만
이 문제는 역발상으로 차가 도착하는 지점을 각 "부분"으로 해석해야 한다.

# 전체 코드

```javascript
function solution(routes) {
  routes.sort((a, b) => a[1] - b[1]);

  let cam = routes.shift()[1];
  let cnt = 1;

  while (routes.length > 0) {
    let [start, end] = routes.shift();
    if (start <= cam) continue;
    else {
      cam = end;
      cnt++;
      continue;
    }
  }

  return cnt;
}
```
