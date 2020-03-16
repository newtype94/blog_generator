---
title: programmers 가장 먼 노드
date: 2020-03-15 10:34:40
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 그래프
---

# 분류 / 레벨 / 언어

그래프 / LV.3 / Javscript

# 설명

## 그래프 용어

정점 vertex
간선 edge
방향성 directed, undirected
사이클 cyclic, acyclic
가중치 weighted
완전(정점,간선 full) complete

## 그래프를 표현하는 자료구조

인접행렬과 인접리스트 방식이 있다.
모든 노드를 탐색할 경우는 두 방식 모두 시간복잡도가 똑같다.

### 인접행렬

방향성 있을 때 시간복잡도 : O(V^2)
방향성 없을 때 시간복잡도 : O(V^2 / 2)

간선밀도가 높은 밀집그래프에 유리

let a: boolean[][] = [[true, false],[false, true]]
let b: int[][] = [[1, 2],[-1, 5]]

1. i에서 j로 방향성 표현 가능
2. 가중치(int) 표현 가능
3. 단 가중치 표현할 때 연결되지 않은 정점간 간선은 -1일지 0일지 상황마다 다름
   (JS는 그냥 숫자 사이에 null 넣어도 될 듯)

### 인접리스트

시간복잡도 : O(V+E)
간선밀도가 낮은 희소그래프에 유리

let a: int[][] = [[2,3],[1], [1,2]]

1. i에서 가지는 값에 대해 방향성 표현 가능
2. 가중치(int) 표현 불가능(값 자리에 tuple을 넣는다면 굳이 가능은 함)

## 문제 풀이

가장 큰 depth를 가지는 노드들을 카운트하는 문제이므로
같은 depth끼리의 이벤트가 중요하다.
그래서 DFS보다는 BFS로 탐색해야 한다.

먼저 BFS의 원칙대로 큐를 사용해 풀어보았다.

1. 최초 노드 insert
2. 맨 앞 노드 out
3. 그 노드의 자손들 insert
4. 큐 empty && 노드 empty => stop

그러나 시간 초과가 발생했다.

```javascript
function solution(n, edge) {
  let node = new Array(n + 1).fill(20000);
  let queue = [1];
  node[0] = 0;
  node[1] = 1;

  while (queue.length > 0) {
    const out = queue.shift();

    edge = edge.reduce((acc, cur) => {
      if (out === cur[0]) {
        queue.push(cur[1]);
        node[cur[1]] = Math.min(node[cur[1]], node[out] + 1);
      } else if (out === cur[1]) {
        queue.push(cur[0]);
        node[cur[0]] = Math.min(node[cur[0]], node[out] + 1);
      } else acc.push(cur);
      return acc;
    }, []);
  }

  return node.filter(v => v === Math.max(...node)).length;
}
```

# 전체 코드

현재 가장 깊은 노드 집합를 set으로 둔다.
그보다 아래로 뻗어나갈 수 있으면 임시 set을 만들어 채워넣는다.
임시 set이 꽉 차면 원래 set에 바꿔 넣는다.

```javascript
function solution(n, edge) {
  let deep = new Set([1]);

  while (edge.length > 0) {
    const temp = new Set([]);

    edge = edge.reduce((acc, cur) => {
      if (deep.has(cur[0]) && deep.has(cur[1])) return acc;
      if (deep.has(cur[0])) temp.add(cur[1]);
      else if (deep.has(cur[1])) temp.add(cur[0]);
      else acc.push(cur);
      return acc;
    }, []);
    if (temp.size > 0) deep = temp;
  }

  return deep.size;
}
```
