---
title: programmers 단어 변환
date: 2020-02-07 17:29:31
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - DFS,BFS
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43163?language=javascript)

# 분류 / 레벨 / 언어

DFS,BFS / LV.3 / Javscript

# 설명

## DFS 풀이

스택을 쓰거나 재귀함수로 푸는 방법 2개가 있다.
이 문제는 재귀함수를 사용하여 풀었다.
재귀함수는 재귀 탈출을 확실히 정의 할 수 있을 때 사용해야 한다.

## BFS 풀이

큐를 사용한다.
BFS는 각 depth가 기준이 되어 형제 노드를 우선으로 탐색한다.
원칙은 queue에서 꺼내면서 해당 노드와 자손관계인 노드들을 insert하지만,
이 문제에서는 depth가 곧 답이 되기 때문에 temp에 넣어두고 한번에 insert했다.

# 전체 코드

## DFS 풀이

```javascript
const oneDiff = (a, b) => {
  let cnt = 0;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) cnt++;
    if (cnt > 1) break;
  }
  if (cnt === 1) return true;
  else return false;
};

function solution(begin, target, words) {
  if (!words.includes(target)) return 0;

  let answer = 50;

  const goNext = (now, remains, cnt) => {
    const nexts = remains.filter(remain => oneDiff(now, remain));
    if (nexts.includes(target)) {
      if (cnt < answer) answer = cnt;
      return;
    }
    nexts.forEach(next => {
      const remainCopy = remains.slice();
      remainCopy.splice(remainCopy.indexOf(next), 1);
      goNext(next, remainCopy, cnt + 1);
    });
  };

  goNext(begin, words, 1);
  return answer;
}
```

## BFS 풀이

```javascript
const oneDiff = (a, b) => {
  let cnt = 0;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) cnt++;
    if (cnt > 1) break;
  }
  if (cnt === 1) return true;
  else return false;
};

function solution(begin, target, words) {
  if (!words.includes(target)) return 0;

  let queue = [begin];
  let level = 0;

  while (1) {
    level++;
    const next = new Set([]);
    while (queue.length > 0) {
      const out = queue.shift();
      const temp = words.filter(word => oneDiff(out, word));
      if (temp.includes(target)) return level;
      else {
        words = words.filter(word => !oneDiff(out, word));
        next.add(...temp);
      }
    }
    queue = [...next];
  }
}
```
