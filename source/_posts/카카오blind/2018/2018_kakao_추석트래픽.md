---
title: 카카오 blind 2018 추석 트래픽
date: 2020-09-08 11:12:45
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17676)

# 문제 풀이

1. 트래픽 시작 시간 순으로 오름차순 정렬한다
2. 트래픽이 빠질 때는 고려하지 않는다. 최댓값을 구하는 것이므로 1이라도 더 큰 순간(트래픽이 들어오는 시점)을 기준으로 잡는다.

# 전체 코드

```javascript
function toSecond(times) {
  const [hour, minute, second] = times.split(":");
  return hour * 3600000 + minute * 60000 + second * 1000;
}

function solution(lines) {
  lines = lines.map((v) => {
    const temp = v.split(" ");
    const end = toSecond(temp[1]);
    const start = end - temp[2].slice(0, -1) * 1000 + 1;

    return [start, end];
  });

  lines.sort((a, b) => a[0] - b[0]);

  let max = 0;

  for (let a of lines) {
    let temp = 0;
    for (let b of lines) {
      if (b[1] >= a[0] - 999 && b[1] <= a[0]) temp++;
      else if (b[0] <= a[0] && b[1] > a[0]) temp++;
    }
    max = Math.max(temp, max);
  }

  return max;
}
```
