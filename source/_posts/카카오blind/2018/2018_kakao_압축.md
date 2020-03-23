---
title: 카카오 blind 2018 압축
date: 2020-03-23 15:51:31
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17684)

# 문제 풀이

두 개의 배열을 사용해야 한다. dic, answer
for문을 돌면서 조건을 검증하고 두 개의 배열 중 한 곳에 넣어준다.
최종적으로 answer를 return한다.

이 문제도 그렇지만,
어떤 한 턴만의 요소를 필요로 하지 않고
앞 뒤 요소를 끌어와 함께 사용해야 하는 경우가 있다.
이럴 때 reduce를 사용하면 조금 더 깔끔해진다.

# 전체 코드

```javascript
function solution(msg) {
  const dic = "~ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
  const answer = [];

  answer.push(
    dic.indexOf(
      msg.split("").reduce((acc, cur) => {
        if (dic.indexOf(acc + cur) > -1) return acc + cur;
        answer.push(dic.indexOf(acc));
        dic.push(acc + cur);
        return cur;
      }, "")
    )
  );

  return answer;
}
```
