---
title: programmers 타겟 넘버
date: 2020-02-02 15:10:12
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - DFS,BFS
---

# 분류 / 레벨 / 언어

DFS,BFS / LV.2 / Javscript

# 설명

## 개요

DFS는 트리가 있을 때 깊은를 우선으로하여
탐색하여 모든 노드를 탐색/검증한다.

이 때, 노드는 physical한 것만을 의미하지는 않는다.
턴제 게임마냥 명백하게 상황이 구분되고, 언젠가 종결되는 것이 자명하면 각 상황을 노드로 봐도 된다.

이 문제에서 요구하는 것은,
한 번씩 더하거나 빼서 원하는 상태가 되는지 판단하는 것이다.

"한 번씩" 이벤트가 누적된 것 = 각 노드

## 풀려면

재귀 함수를 사용한다.
함수 안에 똑같은 함수를 호출하고, 커트하는 조건을 명시하면 된다.

# 전체 코드

```javascript
function solution(numbers, target) {
  let count = 0;
  const end = numbers.length - 1;

  const compare = (depth, added) => {
    if (depth < end) {
      compare(depth + 1, added + numbers[depth + 1]);
      compare(depth + 1, added - numbers[depth + 1]);
    } else if (added === target) {
      count++;
    }
  };
  compare(0, numbers[0]);
  compare(0, -numbers[0]);
  return count;
}
```
