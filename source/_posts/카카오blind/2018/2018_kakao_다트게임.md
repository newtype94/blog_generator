---
title: 카카오 blind 2018 다트게임
date: 2020-04-24 14:11:25
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17682)

# 문제 풀이

구현 문제이다.
결국 dartResult의 모든 요소를 다 점검해야하므로 시간복잡도는 n이 된다.

가능한 가독성 좋게 풀려고 했다. 
1. 10 체크
2. 0-9 체크
3. 이외 문자 체크 => cal() 호출


# 전체 코드

```javascript
function solution(dartResult) {
  const darts = dartResult.split("");
  let scores = [0, 0, 0];
  let i = -1;

  const cal = (input) => {
    switch (input) {
      case "D":
        scores[i] = Math.pow(scores[i], 2);
        break;
      case "T":
        scores[i] = Math.pow(scores[i], 3);
        break;
      case "*":
        scores[i] = scores[i] * 2;
        if (i > 0) scores[i - 1] = scores[i - 1] * 2;
        break;
      case "#":
        scores[i] = scores[i] * -1;
        break;
      case "S":
      default:
        break;
    }
  };

  while (darts.length > 0) {
    const now = darts.shift();
    if (now === "1" && darts[0] === "0") {
      i++;
      darts.shift();
      scores[i] = 10;
    } else if (now < 10) {
      i++;
      scores[i] = parseInt(now);
    } else cal(now);
  }

  return scores.reduce((acc, cur) => acc + cur);
}
```
