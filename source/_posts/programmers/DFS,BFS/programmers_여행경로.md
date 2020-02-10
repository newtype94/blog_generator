---
title: programmers 여행경로
date: 2020-02-10 19:31:10
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스
  - DFS,BFS
---

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
  const next = (hope, remains, route) => {
    if (remains.length > 0) {
      remains.forEach((remain, i) => {
        if (hope === remain[0]) {
          let remainsCopy = remains.concat();
          next(remainsCopy.splice(i, 1)[0][1], remainsCopy, route.concat(hope));
        }
      });
    } else {
      routes.push(route.concat(hope));
    }
  };

  tickets.forEach((ticket, i) => {
    if (ticket[0] === "ICN") {
      let ticketsCopy = tickets.concat();
      next(ticketsCopy.splice(i, 1)[0][1], ticketsCopy, ["ICN"]);
    }
  });

  return routes
    .map(route => route.join())
    .sort()[0]
    .split(",");
}
```
