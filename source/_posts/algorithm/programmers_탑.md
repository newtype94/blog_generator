---
title: programmers 탑
date: 2020-02-03 11:42:12
tags:
  - 알고리즘
category:
  - 알고리즘
  - 프로그래머스
---

# 분류 / 레벨 /언어

스택,큐 / LV.2 / Javscript

# 설명

스택,큐 문제는 주로 "정해진", "순서"등의 키워드가 있다.
JS는 array.push(), array.pop()으로 스택을 사용할 수 있다.
그리고 array.shift()로 큐를 사용할 수 있다.
단 이 문제는 그냥 순리대로 푸는 문제라서
그런 것을 사용하지 않고 그냥 써나갔다.

# 전체 코드

```javascript
function solution(heights) {
  const answer = [];
  heights.forEach((item, index) => {
    if (index === 0) answer.push(0);
    else
      for (let i = index - 1; i > -1; i--) {
        if (heights[i] > item) {
          answer.push(i + 1);
          break;
        } else if (i === 0) answer.push(0);
      }
  });
  return answer;
}
```
