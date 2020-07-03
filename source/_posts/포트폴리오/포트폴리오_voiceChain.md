---
title: 포트폴리오 - voice chain
date: 2020-07-01 15:11:32
tags:
  - React Native
  - AWS
  - lambda
  - dynamodb
category:
  - 포트폴리오
  - 졸업프로젝트
---

# Voice Chain

## 기간

- 제작기간
  2020.01 ~ 2020.06
- 발표
  2020.06.19

## 사용기술

<img src="/image/voiceChain/아키텍처.JPG" width="90%" title="30px" alt="구조도"></img>

|          | 사용 기술                                   |
| -------- | ------------------------------------------- |
| AWS      | lambda, APIgateway, S3, cloudformation(SAM) |
| Frontend | React Native(expo), flexbox                 |
| Backend  | nodeJS                                      |
| Database | dynamodb, sqlite3                           |

## 접근 방향

녹음의 품질, 네트워크 성능 등을 고려하기 보다는
녹음 파일의 무결성을 어떻게 증명할 수 있을지에 대해 고민하고 개발함

## 개발 동기

문제점 : 조작된 녹음 파일로 인한 피해 발생 [예시](https://namu.wiki/w/국민의당%20제보%20조작%20사건)

- 녹음 파일의 무결성을 다자적으로 공증한다면 무결성 증명 가능
- 법정에서 증거로 채택 시 효력 강화
- 블록 체인을 사회적으로 가치 있게 풀어낼 수 있는 개발
- 구두계약과 같이 대화가 중요한 경우 확실한 증거 보전

## 관련 연구

1. 기존의 접근 방법

   - 공인된 속기사가 녹음 파일을 한글 문서로 변환
   - 이 과정을 거쳐야만 증거로서 효력이 생김

2. 보완한 점
   - 녹취속기사에게 녹음 파일을 제출함과 동시에 무결성도 확보한다면 더 강력한 증거가 될 것임

# 개발 계획

## 아이디어

1. 처음 아이디어 : 사용자의 어플리케이션에서 녹음이 완료된 순간 해시값을 획득하여 운영자의 서버에 저장
2. 기업 측 DB를 무조건 신뢰하는 것보다, 더 공증의 효과를 가질 수 있는 방법으로 프라이빗 블록체인의 원리 도입.

## 환경 선택

1. 이더리움 플랫폼을 dappp을 개발하면 트랜잭션마다 "가스"를 지불해야 한다. 결국 유저가 해시를 업로드려면 원치 않아도 비트코인(채굴)을 운용해야만 한다.
2. 그래서 블록체인용 플랫폼을 사용하지 않고 AWS, react native 등으로 직접 구성
3. 하드웨어 선택 => 모바일 기기
   녹음의 대부분이 스마트폰으로 이루어짐
   풀노드를 유지하는 것에 유리함 - 대부분의 스마트폰은 24시간 전원이 유지되고 24시간 인터넷 망에 연결됨 - mobile의 capacity도 pc 못지 않음 (갤럭시 S10+ 기준 최대 1TB)

## 블록 설계

블록체인 네트워크 연결 = websocket 연결
소켓에 연동된 풀노드들과 네트워킹

<img src="/image/voiceChain/블록.JPG" width="100%" title="30px" alt="구조도"></img>

- idx : 블록의 index
- hash : 블록의 sha256 hash 값, 나머지 요소들이 다 존재해야 구할 수 있음
- previousHash : 이전 블록의 hash
- createdAt : 블록 생성 시각
- tx_voiceHash : 음원의 고유 md5 hash 값
- tx_userId : 블록을 생성한 유저의 ID
- tx_timestamp : 녹음 완료 시각

# 기능 구현

## 시뮬레이션 영상 (이미지 클릭)

[![Video Label](http://img.youtube.com/vi/eQBibb1iZX0/0.jpg)](https://www.youtube.com/watch?v=eQBibb1iZX0)

## 풀노드 유지

모든 유저는 블록체인 네트워킹을 위해 풀노드를 유지해야 한다.

<img src="/image/voiceChain/접속절차.JPG" width="100%" title="30px" alt="구조도"></img>

- socket 서버에 접속을 시도할 때
  rest API를 통해 개인 스마트폰의 sqlite에 저장된 블록을 점검하고, 부족한 부분을 보충한다.
- 풀노드임이 확인되어야 socket 서버에 접속할 수 있다.

## 조작 방지

- 녹음 시점 조작 방지 - 녹음이 완료된 즉시 블록체인 네트워크에 해시값을 전파한다.
- 연속성 조작 방지 - 녹음 중간 일시 정지를 할 수 없다.

## Voice record & Add block request

- 녹음이 완료되는 시점에 새 블록을 계산하여 전파한다.
- 녹음하는 동안 상대로 부터 새 블록을 전파 받는 경우 충돌 방지

## recorded file check request

실시간 접속된 유저를 통해 소유한 음원의 원본 여부를 공증 받아 로그로 볼 수 있다.

## record file share

- 녹음 파일을 공유하여 누구나 각자의 핸드폰에서 공증 요청을 보낼 수 있다.
- 녹음 파일의 이름에 고유명, 녹취 제작자, timestamp가 들어가 있다.

## etc

- 내 기기에 저장된 음원 재생 기능, 삭제 기능

# 개발 결과

## Git

[expo App](https://github.com/newtype94/voice_chain_expo_app)
[rest API server](https://github.com/newtype94/voice_chain_rest_api)
[socket API server](https://github.com/newtype94/voice_chain_socket_api)

## Simulation

- SAM template에 아키텍처 구현 후 AWS cloundformation로 프로비저닝
- AWS S3에 script를 업로드하여 serverless 동작
- 스마트폰 환경에 대수 제한이 있어 같은 기능을 하는 로컬 html 시뮬레이터 구현

## 서버 성능, 가격 문제

- 서버 부하는 AWS가 자동으로 판단하여 로드밸런싱이 필요한 경우 Auto-scaling
- AWS 학생 할인으로 무료로 운영

## 추후 할 일

- 악의적인 유저가 리버싱, 와이어샤크 등으로 작동원리의 약점을 파악해 조작된 음원으로 블록을 생성할 경우 방지
- 유저가 극소수일 경우 보증의 효과가 적을 수 있으니, 초기 유저 유입 필요. 접속 시간에 비례한 포인트 제공 등 구현 필요
- 카카오톡과 같이 완전히 종료해도 background에서 동작하도록 구현
