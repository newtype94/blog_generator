---
title: 카카오 blind 2018 자동완성
date: 2020-03-24 12:09:18
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17685)

# 문제 풀이

## 재귀, 조건 검증

재귀안에 재귀를 걸어주는데,
중간에 조건을 검증하여 필터링해야한다.

1. node 요소가 없으면 return
2. idx가 node 요소의 길이보다도 긴 경우 필터링
3. idx의 위치에서 서로 다른 node 필터링 + recur()
4. 남은 node가 하나라면 return, 아니라면 recur()

## 로그 확인

문제에서 요구하는 답은
각 search 입력 수의 합이다.
그런데 각 search 수가 실제랑 다르면서
우연스레 누적 값이 같은 경우도 생길 수 있다.

그래서 첫 줄의 cnt를 0 대신 []로 두고
"cnt+=값"대신 "cnt.push(값)"으로 충분히 확인해본 후
마지막에 "cnt+=값"으로 바꿔서 제출하는 것이 확실하다.

# 전체 코드

```javascript
function solution(words) {
  let cnt = 0;

  const recur = (node, idx) => {
    if (!node[0]) return;

    node = node.reduce((acc, cur) => {
      if (!cur[idx]) cnt += idx;
      else acc.push(cur);
      return acc;
    }, []);

    recur(
      node.filter(v => v[idx] !== node[0][idx]),
      idx
    );
    node = node.filter(v => v[idx] === node[0][idx]);

    if (node.length > 1) recur(node, idx + 1);
    else cnt += idx + 1;
  };

  recur(words, 0);

  return cnt;
}
```
