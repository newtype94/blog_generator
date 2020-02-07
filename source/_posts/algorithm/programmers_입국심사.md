---
title: programmers 입국심사
date: 2020-02-05 17:24:14
tags:
  - 알고리즘
category:
  - 알고리즘
  - 프로그래머스
---

# 분류 / 레벨 / 언어

이분탐색 / LV.3 / Javscript

# 설명

## 문제 독해

문제의 조건을 보면
입국 대기자는 빈 심사장이 생겨도, 기다린 후에 더 빠른 심사장을 선택할 수 있다.
여기서 오해의 소지가 발생하는데,
그런 선택이 가능할 뿐이지 대기자가 매순간 자신에게 유리한 선택을 하는 것이 아니다.
문제에 따르면 대기자는 심사 누적시간이 가장 적게 걸리게끔 행동해주어야한다.
(굳이 말하자면 공항 측에 이득이 되게.. 이런게 문제의 억지임)
만약 제대로 독해하지 못했다면, 이분탐색이 아니라 while(n>0){time--} 이런 구현 문제로 풀게 된다.

## 문제 풀이

도출될 수 있는 심사 시간 list 중 가장 최선의 시간을 골라야 한다.
이분탐색의 특성상 가능한 답의 리스트를 쭉 뽑아두고
또 역으로 대입하고, 범위를 줄이고를 반복하여 풀 것이다.

역으로 대입하기 위한 계산 방정식을 먼저 만들자.

```javascript
const cal = x => times.reduce((acc, curr) => acc + Math.floor(x / curr), 0);
```

cal(x)을 돌렸을 때 사람수를 리턴한다. x는 가능한 제일 작아야 한다.

# 전체 코드

```javascript
function solution(n, times) {
  times.sort((a, b) => a - b);

  if (n === 1) return times[0];

  const cal = x => times.reduce((acc, curr) => acc + Math.floor(x / curr), 0);
  let min = 0; //가장 이상적인 경우 : 프리패스
  let max = times[times.length - 1] * n; //느린애한테만 심사받음

  while (1) {
    if (max - min === 1) return max;
    const mid = Math.floor((min + max) / 2);
    cal(mid) < n ? (min = mid) : (max = mid);
  }
}
```
