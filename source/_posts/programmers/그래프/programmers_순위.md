---
title: programmers 순위
date: 2020-03-17 11:31:34
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

## 인접 행렬

인접 행렬 adjacent matrix를 사용한다.
(행,열)을 (a,b)라고 할 때 a가 b를 이기면 1, a가 b에게 지면 -1을 저장한다.
비기는 경우는 없으므로 생각하지 않는다.
a와 b의 승패를 도저히 알 수 없을 경우 0(default)을 저장한다.

그리고 배열의 index에 편하게 접근하기 위해 (n+1)x(n+1) 규모의 인접 행렬을 사용한다.

## 풀이 과정

1. input만으로도 알 수 있는 승패 결과는 인접 행렬에 저장한다.
2. 3중첩 반복문으로 (a,b) 위치에서 다른 행에 접근해 승패 정보를 전파한다.
   (like [플로이드와샬](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%85%9C_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98))
3. 3중첩이나 했기 때문에 전파 과정에 빈틈이 생길 수 없다.
   (input을 하나씩 추출하면서 정보를 전파했을 때는 빈틈이 생겼다.)
4. 최종 카운트할 때는 index = 0, index_x === index_y 인 경우를 봐줘야 하므로
   0이 2개인 행을 카운트한다.

# 전체 코드

```javascript
function solution(n, results) {
  const adj = new Array(n + 1).fill(0).map(v => new Array(n + 1).fill(0));

  while (results.length > 0) {
    const [a, b] = results.shift();
    adj[a][b] = 1;
    adj[b][a] = -1;
  }

  for (let a in adj) {
    if (a === 0) continue;
    for (let b in adj[a]) {
      if (b === 0 || a === b || adj[a][b] < 1) continue;
      for (let i = 1; i <= n; i++) {
        if (adj[i][a] === 1) {
          adj[i][b] = 1;
          adj[b][i] = -1;
        }
      }
    }
  }

  return adj.filter(x => x.filter(y => y === 0).length === 2).length;
}
```
