---
title: programmers 타일 장식물
date: 2020-02-10 19:51:20
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스
  - 동적계획법(Dynamic Programming)
---

# 분류 / 레벨 / 언어

동적계획법(Dynamic Programming) / LV.3 / Javscript

# 설명

DP문제는 계산한 값들을 어딘가에 저장해두고 다시 읽어오는 방식으로 푼다.
다른 알고리즘 문제들이 count++을 하거나, 누적 값들을 넘겨가며 처리했다면
DP는 "언제" 계산했는지와 "어떤"값인지 까지 메모리에 올려 둔다.

문제를 독해하고
아 몇 턴 지나면 이 값 또 써야하는데?? 
싶으면 DP로 문제를 풀자!

# 전체 코드

```javascript
function solution(N) {
  if(N === 1) return 4;
  const squares = [1,1];
  let count = 2;

  while (N > count){
    squares.push(squares[count - 1] + squares[count - 2]);
    count++;
  }

  return squares[count - 1] * 4 + squares[count - 2] * 2;
}
```
