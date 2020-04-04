---
title: programmers 섬 연결하기
date: 2020-03-03 17:20:31
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42861)

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.3 / Javscript

# 설명

이 문제에서 기준이 되는 것은
각 노드가 아니라
노드을 연결하는 간선이 되어야 한다.

이것을 시행착오를 겪고 알았다.

## 노드를 기준으로

처음엔 노드를 기준으로 그리디를 적용해보았다.

1. 각 노드에서 가장 짧은 간선을 찾아 건너간다.
2. 건너간 노드에서 또 최소 간선을 찾아 건너간다.
3. 건너간 노드에서 갈 수 있는 간선이 없다면 index=0부터 index++하여 다음 노드로 기준을 옮긴다.

이렇게 풀면 백프로 연결하는 것은 보장되지만 최소가 아닐 수 있다.

(사이클)
0-1 : 2
1-2 : 4
2-3 : 5
3-4 : 6
4-1 : 3

이 경우 0부터 시작하면 2 4 5 6 간선을 건너갈 것이다.
그러나 3-4 대신 4-1을 연결하는 것이 더 최적의 경로이므로
이 방법으로는 정답을 도출할 수 없다.

## 간선을 기준으로

1. 간선을 기준으로 costs 배열을 오름차순 정렬한다.
2. costs 앞요소부터 꺼내서 sum에 더 해나간다.
3. 모든 노드가 연결되었을 때 종료한다.

간단해보이지만 3번이 어렵다.

[노드] -- 1 -- [노드] -- 9 -- [노드] -- 1 -- []

위 그래프에서 1 두 개를 먼저 잇고 9를 이어야 종료될 것이다.
그런데 1 두 개를 이었을 때 이미 모든 노드를 방문한 시점이 되는데,
이것은 종료 타이밍과 별개로 생각해야 한다.
일단 연결된 노드 집단을 각각 별도의 섬으로 봐야하고,
모든 섬들이 이어져 하나의 섬이 되었을 때(섬에 모든 노드가 들어왔을때) 종료해야 한다.

# 전체 코드

```javascript
function solution(n, costs) {
  if (n === 1) return 0;
  costs.sort((a, b) => a[2] - b[2]);

  const tmp = costs.shift();
  let con = new Set([new Set([tmp[0], tmp[1]])]);
  let sum = tmp[2];

  while (1) {
    if ([...con][0].size === n) break;
    const [a, b, val] = costs.shift();
    if ([...con].some(v => v.has(a) && v.has(b))) continue;
    sum += val;

    const conA = [...con].find(v => v.has(a));
    if (conA) con.delete(conA);
    const conB = [...con].find(v => v.has(b));
    if (conB) con.delete(conB);

    if (conA && conB) con.add(new Set([...conA, ...conB]));
    else if (conA) con.add(new Set([...conA, b]));
    else if (conB) con.add(new Set([...conB, a]));
    else con.add(new Set([a, b]));
  }

  return sum;
}
```
