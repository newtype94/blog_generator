---
title: programmers K번째 수
date: 2020-01-25 11:35:19
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 정렬
---

# 분류 / 레벨 / 언어

정렬 / LV.1 / Javscript

# 설명

코딩테스트 준비에 입문한다면 가장 먼저 풀어보아야 할 문제이다.
이 문제는 특히 해야할 일을 input에 명시적으로 적어주었다.
commands를 여러 command로 분리하고
array를 특정 구간 command[0],command[1] 사이로 자른 후,
정렬하여,
command[2] 위치를 출력한다.
각 언어의 기본 문법만 알면 풀 수 있다!

# 전체 코드

```javascript
function solution(array, commands) {
  return commands.map(
    v => array.slice(v[0] - 1, v[1]).sort((a, b) => a - b)[v[2] - 1]
  );
}
```

```javscript
function solution(numbers) {
    const compare = (a,b)=>{
       a = String(a)
        b= String(b)
        let x = 0;
        let y = 0;
        while(a[x]===b[y]){
            if(x < a.length-1) x++
            if(y < b.length-1) y++
        }

      return b[y]-a[x];
    }

    return numbers.sort(compare).join("")
}
```
