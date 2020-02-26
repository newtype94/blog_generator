---
title: programmers 카드 게임
date: 2020-02-26 12:50:12
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 동적계획법(Dynamic Programming)
---

# 분류 / 레벨 / 언어

동적계획법(Dynamic Programming) / LV.4 / Javscript

# 설명

## 처음 풀이

먼저, 빠르게 구현할 수 있고 모든 요소를 검증할 수 있는 재귀로 풀었다.
그러나 left와 right의 최대 길이가 각 1000개씩이고,
left[0] >= right[0] 일 경우 최대 2개씩 갈라지므로
최대 2의 1000제곱 만큼의 loop 발생한다.
돌려보니 역시나 시간 초과가 발생했다.

```javascript
function solution(left, right) {
  let max = 0;

  const next = (l, r, sum) => {
    if (l.length * r.length === 0) {
      if (sum > max) max = sum;
      return;
    }

    let lShift = l.slice(1, l.length);
    let rShift = r.slice(1, r.length);

    if (l[0] > r[0]) next(l, rShift, sum + r[0]);
    else {
      next(lShift, r, sum);
      next(lShift, rShift, sum);
    }
  };

  next(left, right, 0);
  return max;
}
```

## DP로 풀어야 하는 이유

2의 1000제곱은 어마어마하게 큰 수지만,
2차원 배열의 크기인 1000 x 1000은 백만으로 비교적 다룰만한 수이다.
그리고 2차원 배열의 각 칸에 저장되는 값들도
1~2000 사이 정수들의 합으로 구성되므로
공간복잡도도 비교적 작은 편이다.

left(left_index) > right(right_index) 일 경우 무조건 sum에 더하고

# 전체 코드

```javascript
function solution(left, right) {
  const length = left.length;
  const memo = new Array(length + 1).fill(new Array(length + 1).fill(-1));
  console.log(memo);

  const next = (l, r) => {
    if (l === length || r === length) {
      return;
    }

    if (memo[l][r] > -1) return;
    if (l === 1 && r === 1) return 0;
    if (left[l])
      if (left[l] > right[r]) next(l, rShift, sum + r[0]);
      else {
        next(lShift, r, sum);
        next(lShift, rShift, sum);
      }
  };

  next(1, 1);
  return memo;
}

console.log(solution([1, 1, 9, 1, 1], [8, 9, 2, 2, 2]));
```
