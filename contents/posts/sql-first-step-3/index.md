---
title: "[SQL 첫걸음] 3. 정렬과 연산"
description: "MySQL 페이지네이션 기본기 ORDER BY, LIMIT, OFFSET"
date: 2024-06-09 17:52:34
update: 2024-06-09 17:52:34
tags:
  - SQL
series: SQL 첫걸음 
---

MySQL에서 페이지네이션을 구현할 때 LIMIT과 OFFSET을 사용한다. 이번 장에서는 정렬에 대해 알아보자.

## 정렬 - ORDER BY

```sql
SELECT 열명
FROM 테이블명
WHERE 조건식
ORDER BY 열명;
```

- **ORDER BY는 검색 결과의 행 순서를 바꾸는 데 사용된다.**
- 테이블에 저장된 데이터의 순서를 바꾸지 않는다.
- 지정하는 열명을 기준으로 정렬한다.
- 기본은 오름차순(ASC)이고, 내림차순은 DESC 키워드를 사용한다.
- 가능한 정렬 방법을 생략하지 않고 지정하는 방법을 권장한다.

```sql
SELECT 열명
FROM 테이블명
WHERE 조건식
ORDER BY 열명1, 열명2;
```

- 복수의 열을 지정하여 정렬할 수 있다.
- **NULL 값의 정렬순서는 DBMS마다 다르다. MySQL은 NULL 값이 가장 작은 값으로 취급한다.**

## 결과 행 제한하기 - LIMIT & OFFSET

```sql
SELECT 열명
FROM 테이블명 LIMIT 행수
OFFSET 위치;
```

- 결과로 반환되는 행 수를 제한하는 데 사용한다.
- LIMIT 구는 표준 SQL이 아니다. MySQL, PostgreSQL에서 사용할 수 있다.
- OFFSET 다음에는 시작 위치를 지정한다.
- **LIMIT과 OFFSET은 페이지네이션(Pagination)에 사용한다.**
