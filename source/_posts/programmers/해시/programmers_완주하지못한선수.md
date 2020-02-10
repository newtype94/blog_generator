---
title: programmers 완주하지 못한 선수
date: 2020-02-01 12:32:13
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스
  - 해시
---

# 분류 / 레벨 / 언어

해시 / LV.1 / Javscript

# 설명

이렇게만 돌려도 충분한가? 반례나 특수한 경우는 없나?
라고 고민이 드는 문제들이 많은데 이 문제는 그렇지 않았다.

완주하지 못한 사람(미완주자)가 딱 한 명이라서
미완주자가 없는 경우를 생각할 필요도 없고, 한 명을 찾고 그 뒤로 또 찾을 필요도 없다.
그래서 이런 경우는 while문 안에서 과감하게 return시켜도 된다.

# 전체 코드

```javascript
function solution(participant, completion) {
  participant.sort();
  completion.sort();
  let i = 0;
  while (1) {
    if (participant[i] !== completion[i]) return participant[i];
    i++;
  }
}
```
