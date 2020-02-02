---
title: programmers 베스트앨범
date: 2020-02-02 14:46:24
tags:
  - 알고리즘
category:
  - 알고리즘
  - 프로그래머스 문제풀이
---

# 분류 / 언어

해시 set / Javscript

# 설명

자료구조는 2개를 썼다. (genreHits, songHits)

1. 노래 한 곡에 대한 정보들을
   2번에 거쳐 input으로 주었으므로 묶어주는 과정이 필요하다.
   => songHits 객체에 {장르1 : [{1번트랙}, {2번트랙}]}와 같이 넣어준다.
2. 장르에 대해 플레이수 누적을 해야한다.
   => songHits에서 장르별로 reduce()를 돌려 플레이수를 누적한 후,
   genreHits에 [{1번 장르}, {2번 장르}]와 같이 넣어준다.

# 전체 코드

```javascript
function solution(genres, plays) {
  const answer = [];
  const genreHits = new Array();
  const songHits = new Object();

  genres.forEach((item, index) => {
    songHits[item]
      ? songHits[item].push({ index: index, plays: plays[index] })
      : (songHits[item] = [{ index: index, plays: plays[index] }]);
  });

  for (let key in songHits) {
    genreHits.push({
      genre: key,
      plays: songHits[key].reduce((acc, curr) => acc + curr.plays, 0)
    });
  }
  genreHits.sort((a, b) => b.plays - a.plays);

  while (genreHits.length !== 0) {
    let temp = songHits[genreHits.shift().genre].sort(
      (a, b) => b.plays - a.plays
    );
    if (temp.length > 1) {
      answer.push(temp[0].index);
      answer.push(temp[1].index);
    } else {
      answer.push(temp[0].index);
    }
  }

  return answer;
}
```
