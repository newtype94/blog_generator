---
title: 카카오 blind 2019 크레인 인형뽑기 게임
date: 2020-06-11 11:01:33
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2019 인턴
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64061)

# 문제 풀이

두 가지를 할 수 있어야 한다.

1. input으로 주어진 board 변수를 N x N 격자 판 전용 2차원 배열에 새로 배치하기.
2. 바구니를 stack으로써 사용하고, 빼내는 조건을 구현하기

# 전체 코드

```javascript
function solution(board, moves) {
  let answer = 0;
  const pan = new Array(board[0].length).fill([]).map((v) => []);
  const outBox = [];

  while (board.length > 0) {
    const row = board.pop();
    row.forEach((v, i) => {
      if (v !== 0) pan[i].push(v);
    });
  }

  while (moves.length > 0) {
    const out = pan[moves.shift() - 1].pop();
    if (!out) continue;
    if (outBox.length < 1 || out !== outBox[outBox.length - 1])
      outBox.push(out);
    else {
      outBox.pop();
      answer += 2;
    }
  }

  return answer;
}
```
