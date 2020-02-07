---
title: programmers 예산
date: 2020-02-05 15:33:34
tags:
  - 알고리즘
category:
  - 알고리즘
  - 프로그래머스
---

# 분류 / 레벨 / 언어

이분탐색 / LV.3 / Javscript

# 설명

## 이분탐색 이론

left(변수), right(변수)를 딱 필요한 만큼의 범위를 커버할 수 있게 잡아준다.
middle(변수) = 소수점버림(left+right/2)로 잡는다.
루프를 돌면서 middle이 어떤 조건에 맞는지 판단하고 left또는 right에 넣어준다.

ex)
1,2,3, ... , 98, 99, 100

문제의 요구사항을 분석해 left, right를 잡아준다. (예시로 2, 98)
그리고 middle을 바로 계산해 left와 right 중 어디로 넣어줄지 결정한다.

2 ------ 98 ( => 50 )
2 ------ 50 ( => 26 )
2 ------ 26 ( => 14 )
14 ------ 26 ( => 20)
...

## 문제풀이

이분탐색은 문제없이 짠 것 같은데
정확성 케이스와 효율성 테스트에서 계속 한 개씩 통과가 안되었다.
온갖 수정을 거듭한 끝에, 기본적인 것을 놓치고 있다는 생각이 들어 한줄한줄 로그를 찍어보았다.

다시 보니 처음에 그냥 sort()를 호출했다.
그냥 sort()를 하면, [1,3,2,10000]가 문자열 순으로 [1,10000,2,3] 이렇게 정렬된다.
(19 하반기 코테도 이거 때문에 떨어진듯...)
sort((a,b)=>a-b)로 숫자오름차순 정렬!

# 전체 코드

```javascript
function solution(budgets, M) {
  budgets.sort((a, b) => a - b);

  const sumByLimit = limit =>
    budgets.reduce((acc, curr) => (curr <= limit ? acc + curr : acc + limit));

  let left = Math.floor(M / budgets.length); //이론적 최소치
  let right = budgets[budgets.length - 1]; //이론적 최대치

  //아래부터는 left로 거를예정이라 right를 최초에 한번 걸러주어야함
  if (sumByLimit(right) <= M) return right;

  while (1) {
    if (sumByLimit(left + 1) > M) return left;
    const mid = Math.floor((left + right) / 2);
    sumByLimit(mid) <= M ? (left = mid) : (right = mid);
  }
}
```
