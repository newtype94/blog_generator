---
title: Database - SQL vs NOSQL
date: 2020-05-15 10:50:15
tags:
  - Database
category:
  - Database
---

# SQL

## 장점

1.  엄격한 스키마

    - 데이터 무결성 보장
    - 관계는 각 데이터를 중복없이 한번만 저장

## 단점

1. RDB이므로 관계를 맺고 있음

   - JOIN문이 많은 복잡한 쿼리가 생길 수 있음

2. 수평적 확장(Scale out) 어려움, 수직적 확장(Scale up) 가능

   - 수직정 확장 = 하드웨어 업그레이드

## 도입

- relational 데이터가 자주 변경 되는 경우(NoSQL은 여러 컬렉션을 모두 update해야함)
- 스키마가 확정되어 잘 바뀔 일이 없는 경우(대기업)

# NoSQL

## 장점

1. 스키마 없음

   - 데이터 수정이 자유롭고, "필드(컬럼)" 관리도 쉬움

2. database > collections > documents 구조(mongoDB)

   - document : key-value형태의 BSON(Binary JSON). 쿼리 속도 빠름

3. 수직 확장, 수평 확장 쉬움

## 단점

1. data update 불리함

- 댓글 컬렉션 => {댓글:A}
- 글 컬렉션 => {글:ㄱ, {댓글:A}}
- 데이터가 여러 컬렉션에 중복되어 n번 수행해야 함

## 도입

- 데이터 구조를 한번에 확정할 수 없고, 추후 변경 / 확장 될 수 있는 경우(스타트업)
- read는 자주 하고, update는 잘 안하는 경우
- 트래픽이 많아 분산 디비가 필요한 경우

## 종류

- Key-value(Memcached, Redis, Amazon Dynamo DB)
- Document(MongoDB)
- Column-family(HBase)
- Graph

- 그래프를 제외한 세 모델은 집합-지향(Aggregate-oriented) 모델

# ORM

## Object Relational Mapping

1. DB의 schema를 class에 매핑. => DB mingration, 객체 생성
2. query 대신 함수와 객체를 사용해 DB에 접근한다.(생산성 증가)

## 도입

1. 일단 nosql 보다 RDB가 더 유리한 상황일 때
2. 객체 지향적인 코드로 직관적이고 생산적인 개발을 하고 싶을 때
