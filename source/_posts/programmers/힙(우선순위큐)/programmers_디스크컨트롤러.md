---
title: programmers 디스크 컨트롤러
date: 2020-02-03 14:05:34
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 힙(우선순위큐)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42627)

# 분류 / 레벨 / 언어

힙(우선순위큐) / LV.3 / Javscript

# 설명

JS는 C++과 같이 STL로 제공되는 우선순위큐가 없다!
대신 코테에서 실행시간을 넉넉히 주므로 걱정할 것도 없다!

이 문제에서는 우선순위큐에 "in" 이벤트가 발생할 때,
큐.sort(콜백)으로 원하는 요소를 기준으로 정렬했다. (이런 경우, 콜백을 야무지게 써야한다)

또한 원래 배열에서 "out" 이벤트가 발생할 때,
array베타 = array알파.reduce()로 다음 턴에 접근시 시간을 줄였다.

# 전체 코드

```javascript
function solution(jobs) {
  let time = 0;
  let sum = 0;
  const divide = jobs.length;
  const waiting = [];

  while (jobs.length > 0 || waiting.length > 0) {
    jobs = jobs.reduce((acc, curr) => {
      if (curr[0] <= time) {
        waiting.push(curr);
        waiting.sort((a, b) => a[1] - b[1]);
      } else acc.push(curr);
      return acc;
    }, []);

    if (waiting.length > 0) {
      let out = waiting.shift();
      time += out[1];
      sum += time - out[0];
    } else time++;
  }

  return Math.floor(sum / divide);
}
```
