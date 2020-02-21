---
title: programmers 구명보트
date: 2020-02-15 15:53:28
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

그리디 알고리즘에서 우선순위로 둘 만한것 = 처리하기 쉬운 요소, 놔두면 피곤해지는 요소
이 문제에서는 비교적 무거운 사람을 우선순위로 둘 만하다.

오름차순으로 정렬하여,
pop()한 사람을 먼저 태우고, 그 위에 가벼운 사람을 가능한 실어서 출발시킬 것이다.

# 전체 코드

```javascript
function solution(people, limit) {
  let boat = 0;
  let sum = 0;

  people.sort((a, b) => a - b);

  while (people.length > 0) {
    if (sum === 0) {
      boat++;
      sum += people.pop();
    } else {
      while (sum < limit) {
        if (people[0] && sum + people[0] <= limit) sum += people.shift();
        else break;
      }
      sum = 0;
    }
  }
  return boat;
}
```
