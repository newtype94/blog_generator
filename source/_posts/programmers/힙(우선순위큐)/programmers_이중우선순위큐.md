---
title: programmers 이중우선순위큐
date: 2020-02-03 14:05:34
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 힙(우선순위큐)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42628)

# 분류 / 레벨 / 언어

힙(우선순위큐) / LV.3 / Javscript

# 설명

## 힙

- 힙을 BFS식으로 나열했을 때, 오름차순or내림차순 정렬을 보장하지는 않는다!
  단, 부모와 자손간의 관계가 확실하기 때문에 루트가 최댓값or최솟값인 것은 보장한다.

- 힙에 자료를 넣을 때

  1. 마지막 index에 넣고(큐 맨 뒤에 넣듯)
  2. 부모-자손 간 상향식 비교

- 힙에서 자료를 빼낼 때 :

  1. 최댓값or최솟값인 루트만 빼낼 수 있고 (큐가 맨 앞을 꺼내듯)
  2. 루트가 빈자리가 되면 맨 뒷 값을 빼서 가져온다.
  3. 그리고 하향식으로 부모-자손간 비교를 한다.

- 상향식, 하향식 비교가 발생하면 버블 소트와 같이 주체는 자신에게 맞는 자리를 찾아간다.

## 문제풀이

이중우선순위큐라는 자료형이 있었나? 싶었는데 그건 아니었다.
그냥 문제 이름이다.
최대힙, 최소힙 두 개를 굴려가며 풀려했지만
그러기 위해서는 두 힙의 요소들이 매 번 동기화는 것이 상당히 복잡했다.
그래서 그냥 구현식으로 풀었다!

# 전체 코드

```javascript
function solution(operations) {
  const numbers = [];
  while (operations.length > 0) {
    let out = operations.shift();
    switch (out) {
      case "D 1":
        if (numbers.length > 0) numbers.pop();
        break;
      case "D -1":
        if (numbers.length > 0) numbers.shift();
        break;
      default:
        numbers.push(parseInt(out.slice(2, out.length)));
        numbers.sort((a, b) => a - b);
        break;
    }
  }

  const answer = [];
  if (numbers.length > 0) answer.push(numbers.pop());
  else answer.push(0);
  if (numbers.length > 0) answer.push(numbers.shift());
  else answer.push(0);
  return answer;
}
```
