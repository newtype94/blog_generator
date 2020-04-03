---
title: programmers 다리를 지나는 트럭
date: 2020-02-03 12:14:00
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 스택, 큐
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42583)

# 분류 / 레벨 / 언어

스택,큐 / LV.2 / Javscript

# 설명

스택, 큐를 사용하여 상황을 잘 표현해야 하는 문제이다.
while{} 안에서 time++를 하여 타이머를 잰다.
그리고 while{} 안에서 1초 동안 발생하는 이벤트를 표현해주면 된다.

# 전체 코드

```javascript
function solution(bridge_length, weight, truck_weights) {
  let time = 0;
  const bridge = new Array(bridge_length).fill(0); //다리 모형
  let sumOnBridge = 0; //다리 위 무게 합

  do {
    time++;
    let out = bridge.shift();
    if (out > 0) sumOnBridge -= out;
    if (sumOnBridge + truck_weights[0] <= weight) {
      let truckIn = truck_weights.shift();
      bridge.push(truckIn);
      sumOnBridge += truckIn;
    } else bridge.push(0);
  } while (sumOnBridge > 0);

  return time;
}
```
