---
title: programmers 큰 수 만들기
date: 2020-02-11 13:12:40
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.2 / Javscript

# 설명

처음에는 자료구조를 따로 두지 않고,
input으로 들어온 number 하나로 풀었다.
그러니 필요이상으로 루프를 돌게되어 시간복잡도가 매우 커졌다.

정답으로 return할 스택을 하나 추가하고,
k가 남아있을 동안, 'pop() 이벤트= k 차감'으로 풀었다

# 전체 코드

```javascript
function solution(number, k) {
  const answer = number.split("").reduce((acc, curr) => {
    if (k > 0) {
      let i = acc.length - 1;
      while (i > -1 && k > 0 && acc[i] < curr) {
        acc.pop();
        k--;
        i--;
      }
    }
    acc.push(curr);
    return acc;
  }, []);

  return answer.slice(0, answer.length - k).join("");
}
```
