---
title: programmers 가장 큰 수
date: 2020-01-29 13:51:26
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 정렬
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42746)

# 분류 / 레벨 / 언어

정렬 / LV.2 / Javscript

# 설명

정렬 문제이나, Greedy한 시각도 필요하다.
자릿수가 다른 수를 받아도 모두 처리할 수 있는 정렬 알고리즘을 구현하려 했으나
고려할 경우의 수가 너무 많고, 심지어 수도 1000까지 밖에 안주어져서
그냥 매 sort시 최선의 선택을 하도록 만들었다.

답을 제출하고 다른 사람들의 코드를 보았는데 다음과 같은 형변환 트릭이 유행이었다.
`1 * 문자열 => 숫자`
`"" + 숫자 => 문자열`

# 전체 코드

```javascript
function solution(numbers) {
  if (numbers.every(v => v === 0)) return "0";

  return numbers
    .sort((a, b) => {
      a = String(a);
      b = String(b);
      return parseInt(a + b) > parseInt(b + a) ? -1 : 1;
    })
    .join("");
}
```
