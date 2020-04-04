---
title: programmers 여행경로
date: 2020-02-10 19:31:10
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - DFS,BFS
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43164)

# 분류 / 레벨 / 언어

DFS,BFS / LV.3 / Javscript

# 설명

DFS 문제를 재귀로 풀 때는 보통 이런 틀을 갖추고 푼다.

```javascript
let count = 0;
const dfs = (상태, 누적 정보)=>{
  if() dfs(다음 상태, 누적 정보)
  if() count++
}
dfs(초기 상태, 초기 정보)
```

# 전체 코드

```javascript
function solution(tickets) {
  const routes = [];

  const next = (now, remains, route) => {
    if (remains.length > 0) {
      remains
        .filter(v => v[0] === now)
        .forEach((remain, i) => {
          let temp = remains.slice();
          temp.splice(i, 1);
          next(remain[1], temp, route.concat(now));
        });
    } else {
      routes.push(route.concat(now));
    }
  };

  tickets
    .filter(v => v[0] === "ICN")
    .forEach((ticket, i) => {
      let temp = tickets.slice();
      temp.splice(i, 1);
      next(ticket[1], temp, ["ICN"]);
    });

  return routes
    .map(route => route.join(","))
    .sort()[0]
    .split(",");
}
```
