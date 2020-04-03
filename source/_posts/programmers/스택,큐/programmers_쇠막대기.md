---
title: programmers 쇠막대기
date: 2020-02-16 14:40:53
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 스택, 큐
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42585)

# 분류 / 레벨 / 언어

스택,큐 / LV.2 / Javscript

# 설명

## 아이디어

문제에서도 가이드하듯, `()`를 빔으로 치환하는 것이 최우선이다.
단 치환이라고해서 `()`를 굳이 다른 값으로 replace하기 보다는
배열에서 `,` 정도로 생각하는 편이 낫다. = string.split("()")

## 풀이 방법

1. 배열의 요소를 하나씩 돌면서 `(`에는 stack push, `)`에는 stack pop한다.
2. 각 차례가 끝날 때 = `,`에 도달할 때 = 빔
   stack의 개수만큼 더한다.
3. 단 stack을 참고할 때는 pop이 된 후라 막대가 한개가 빠지는 셈이다.
   그래서 pop이벤트마다 미리 answer++ 해준다.

# 전체 코드

```javascript
function solution(arrangement) {
  let arr = arrangement.split("()");
  let answer = 0;
  let stack = 0;

  while (arr.length > 0) {
    arr
      .shift()
      .split("")
      .forEach(v => {
        if (v === "(") stack++;
        else {
          stack--;
          answer++;
        }
      });
    answer += stack;
  }
  return answer;
}
```
