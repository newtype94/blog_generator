---
title: Database - Index
date: 2019-11-30 11:12:41
tags:
  - Database
category:
  - Database
---

# DB에서 자료를 검색하는 두 가지 방법

- FTS(Full Table Scan)
- Index Scan

# Index

- 특정 컬럼을 선택하여 indexing 하면 그 컬럼을 기준으로 정렬된 하나의 테이블이 생김(자원 소모)
- 새로 생긴 테이블은 기존 테이블의 block(데이터가 저장되는 최소 단위) 주소를 가짐. ( 1 block = n x rows)

# Index 설정 팁

- 조건(where)절에 자주 등장하는 컬럼
- order by 절에 자주 등장하는 컬럼(인덱스는 정렬되어 저장되므로)
- 여러 컬럼을 조합해서 만들 수도 있음

## Index 단점

select는 빨라지지만 insert나 update는 느려진다.
기존 테이블 뿐 아니라 index 테이블에도 insert, update 해야 하고,
어느 자리에 insert할지 찾아야 하고, 정렬된 상태를 유지해야 하기 때문

## Index 손익분기점

Index되는 각각의 양이 테이블이 가지고 있는 전체 데이터 양의 10에서 15프로 일때 이득이고,
그 이상일 떈 풀스캔이 더 빠르다.

## Index의 자료구조 = B tree

- B 트리는 하나의 노드에 여러개의 데이터를 저장할 수 있다.
- 하나의 노드에 최대로 저장할 수 있는 데이터의 수 = order(m)
- 각 노드는 최대 m개의 자식을 가질 수 있다.
- Root node와 leaf node를 제외한 모든 노드는 반드시 m/2 개의 자식 노드를 가져야 한다.
- B 트리의 root node는 반드시 두 개 이상의 자식 노드를 가져야 한다.
- 모든 leaf node는 같은 레벨에 위치해야 한다.

## sql

```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);

--MySQL:
ALTER TABLE table_name
DROP INDEX index_name;
```
