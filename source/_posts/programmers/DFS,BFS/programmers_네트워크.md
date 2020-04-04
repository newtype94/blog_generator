---
title: programmers 네트워크
date: 2020-02-04 13:11:19
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - DFS,BFS
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43162)

# 분류 / 레벨 / 언어

DFS,BFS / LV.3 / Javscript

# 설명

같은 카테고리의 타겟넘버 문제는 처음 DFS 호출이 정적으로 정해져 있었으나,
이 문제는 while문안에서 동적으로 DFS를 호출한다.
그 이유는

1. input에 따라서 네트워크 맵의 연결 set이 다르다.
2. 한 set을 다 탐색하고 다음 set을 탐색해야 하는데, 다음 set의 시작노드가 매번 다를 수 밖에 없다.

# 전체 코드

```javascript
function solution(n, computers) {
  let count = 0;
  const visited = new Array(n).fill(false);

  const dfs = (curr, acc) => {
    computers[curr].forEach((connected, i) => {
      if (!visited[i] && connected) {
        visited[i] = true;
        dfs(i, acc.concat(i));
      }
    });
  };

  while (visited.some(data => !data)) {
    const notVisited = visited.indexOf(false);
    dfs(notVisited, [notVisited]);
    count++;
  }

  return count;
}
```
