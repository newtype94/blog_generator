---
title: voiceChain(2) - 초기 setup
date: 2020-01-21 17:57:11
tags:
  - 개발노트
category:
  - 개발노트
  - voiceChain
---

# Front setup

expo!

# Backend setup

socket.io는 단독으로 사용할 수 없다.
express 서버에 붙이는 방식으로 사용한다.
보통 express-generator 모듈로 setup하는데
나는 typescript로 개발할 것이기 때문에 아래 모듈을 사용!

https://www.npmjs.com/package/express-generator-typescript
