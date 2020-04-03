---
title: programmers 징검다리
date: 2020-02-19 14:08:11
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 이분탐색
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43236)

# 분류 / 레벨 / 언어

이분탐색 / LV.4 / Javscript

# 설명

## 풀이 방법

이 문제는 제거할 돌의 수 n이 input이고,
output은 다음과 같다.

1. 제거할 돌을 어떻게 pick하는지에 따라 여러 경우의 수 존재
2. 각 경우에서, 돌 사이의 거리들 중 최솟값을 저장
3. <최솟값>, <최솟값>, <최솟값>, ... 중 최댓값 반환

요약하자면 돌 사이가 서로서로 최대한 멀게끔 빼내라는 말이다.

## 새로운 함수 정의

우리는 역으로 대입할 것이기 때문에
output으로 가능한 "거리"들이 input이 될 것이다.
그래서 이것을 받을 함수도 하나 더 정의해야 한다.

거리 => { 모든 돌 사이의 거리가 input보다 크거나 같아야 한다. 그만큼 돌을 빼내자(with count++) } => count

그리고 output == n 인 input 중 가장 큰 값을 택하면 된다.

## 애매한 점

이 함수는 실제 돌 사이 거리가 될 수 없는 input을 받아도 output을 return한다.
결론적으로 다대1함수이다.
답이 될 수 있는 input들 중 가장 큰 값을 선택하면 될 것 같은 느낌은 들지만
이 느낌을 말로 설명하기가 은근히 애매하다.
이럴 때는 로그를 찍어보는 것이 확실하다.

다음 코드를 임시로 추가하여 로그를 확인했다.

```javascript
const getN = dist => {
  //...생략
  let exact = false;
  for (let i = 0; i < rocksTmp.length - 1; i++) {
    if (rocksTmp[i + 1] - rocksTmp[i] === dist) {
      exact = true;
      break;
    }
  }
  console.log(dist, rocksTmp, "remove_" + cnt, exact);
  return cnt;
};

for (let i = 1; i < distance + 1; i++) {
  getN(i);
}
```

## 로그

1 [ 0, 5, 19, 28, 34 ] remove_0 false
2 [ 0, 5, 19, 28, 34 ] remove_0 false
3 [ 0, 5, 19, 28, 34 ] remove_0 false
4 [ 0, 5, 19, 28, 34 ] remove_0 false
5 [ 0, 5, 19, 28, 34 ] remove_0 true
6 [ 0, 19, 28, 34 ] remove_1 true
7 [ 0, 19, 28 ] remove_2 false
8 [ 0, 19, 28 ] remove_2 false
9 [ 0, 19, 28 ] remove_2 true
10 [ 0, 19, 34 ] remove_2 false
11 [ 0, 19, 34 ] remove_2 false
12 [ 0, 19, 34 ] remove_2 false
13 [ 0, 19, 34 ] remove_2 false
14 [ 0, 19, 34 ] remove_2 false
15 [ 0, 19, 34 ] remove_2 true
16 [ 0, 19 ] remove_3 false
17 [ 0, 19 ] remove_3 false
18 [ 0, 19 ] remove_3 false
19 [ 0, 19 ] remove_3 true
20 [ 0, 28 ] remove_3 false
21 [ 0, 28 ] remove_3 false
22 [ 0, 28 ] remove_3 false
23 [ 0, 28 ] remove_3 false
24 [ 0, 28 ] remove_3 false
25 [ 0, 28 ] remove_3 false
26 [ 0, 28 ] remove_3 false
27 [ 0, 28 ] remove_3 false
28 [ 0, 28 ] remove_3 true
29 [ 0, 34 ] remove_3 false
30 [ 0, 34 ] remove_3 false
31 [ 0, 34 ] remove_3 false
32 [ 0, 34 ] remove_3 false
33 [ 0, 34 ] remove_3 false
34 [ 0, 34 ] remove_3 true

# 전체코드

```javascript
function solution(distance, rocks, n) {
  if (n === rocks.length) return distance;

  rocks.sort((a, b) => a - b);
  rocks.unshift(0);
  rocks.push(distance);

  let right = distance;
  let left = 1;
  let mid;

  const getN = dist => {
    const rocksTmp = rocks.slice();
    let cnt = 0;
    let idx = 0;
    while (idx < rocksTmp.length - 1) {
      if (rocksTmp[idx + 1] - rocksTmp[idx] < dist) {
        rocksTmp.splice(idx + 1, 1);
        cnt++;
      } else idx++;
    }
    return cnt;
  };

  while (right - left > 1) {
    mid = Math.floor((right + left) / 2);
    getN(mid) > n ? (right = mid) : (left = mid);
  }

  return left;
}
```
