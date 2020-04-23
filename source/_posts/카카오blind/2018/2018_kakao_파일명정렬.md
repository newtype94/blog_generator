---
title: 카카오 blind 2018 파일명 정렬
date: 2020-04-23 12:14:51
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17686)

# 문제 풀이

## mapping

files 원본의 정렬본을 반환해야 하므로
files의 각 file을 직접 HEAD, NUMBER, TAIL로 분리하지 않고
각 file과 필요한 요소로 추가하여 만든 객체를 새로 mapping했다.

## stable sort

[1,1,2,3]을 내림차순으로 정렬하면 [3,2,1,1]이다.
<1,1>은 "내림차순"이라는 조건에 해당되지 않아
[3,2,1,1] 마지막에 <1,1>이 그대로 있다.
그리고 이 <1,1>이 원래의 <1,1>과 같은 순서인지 구별할 수 없다.

하지만 [[1,"ㄱ"], [1,"ㄴ"], [2,"ㄷ"], [3,"ㄹ"]]를
value[0]을 기준으로 내림차순 정렬한다면 (`sort((a,b)=>(b[0]-a[0]))`)
정렬 후 마지막 1이 어디에 있던 1인지 알 수 있다.

이처럼 나머지 요소를 확인 가능한 정렬을 할 때,
서로 정렬될 필요가 없는 요소들은 처음 순서대로 있도록 만드는 것이
stable sort다.

## JS의 stable sort

JS의 내장함수 sort()는 stable sort가 아니다.
운 좋게 stable sort처럼 결과가 나올 수는 있지만
시스템상 이를 보장하지는 않는다.

그래서 처음 Array의 각 index를 mapping해두고
sort의 콜백에서 활용하여
stable sort를 흉내내야 한다.

## 이 문제도 stable sort가 필요한지

TAIL이 정렬의 조건에 아예 들어가지 않고
또 sorted files은 가능한 원래 파일들의 순서를 보존하라고 했다.
즉 채점할 때 TAIL을 통해 원래의 순서가 보존되었는지 판단할 것이다.
sort()의 콜백에 원본 index를 활용하지 않으면
운좋게 stable sort되어 몇 개의 답은 맞을 수 있으나
100% 답이 될 수는 없다.

# 전체 코드

```javascript
function solution(files) {
  return files
    .map((file, index) => {
      return {
        file,
        index,
        head: /[^0-9]+/i.exec(file)[0].toLowerCase(),
        num: parseInt(/[0-9]+/i.exec(file)[0].slice(0, 5)),
      };
    })
    .sort((a, b) => {
      if (a.head > b.head) return 1;
      else if (a.head < b.head) return -1;
      else return a.num - b.num === 0 ? a.index - b.index : a.num - b.num;
    })
    .map((v) => v.file);
}
```
