---
title: "집계와 서브쿼리"
date: 2024-07-06
tags:
  - Database
---

> 이 글은 MySQL을 기준으로 작성됐다. 데이터베이스마다 사용법은 다를 수 있다.

## 1. 집계함수

- 집계함수란 무엇인가? 어떤것이 있는가?
- 집계함수의 예시와 사용

집합 그림

집계 함수는 값 집합을 계산하고 단일 값을 반환한다. 일반적인 함수는 인수로 하나의 값을 지정하는데 반해 집계함수는 집합을 지정한다. 
따라서 집합 함수라고 부르기도 한다. 흔히 데이터의 개수, 최댓값, 최솟값, 평균, 합계등을 계산하는데 사용한다.

SQL을 다룰 때 NULL 값을 주의해야 한다.

### 1.1 COUNT - 행의 개수 구하기

```sql
SELECT COUNT(aggregate_expression)
FROM tables
[WHERE conditions]
[ORDER BY expression [ ASC | DESC]];
```

COUNT는 행의 개수를 구하는데 사용한다. COUNT 함수의 결과는 NULL이 아닌 값만 출력된다.

NULL 예시

### 1.2 SUM - 합계 구하기

```sql
SELECT SUM(aggregate_expression)
FROM tables
[WHERE conditions];
```

합계를 구하는데 사용한다.

### 1.3 AVG - 평균 구하기

```sql
SELECT AVG(aggregate_expression)
FROM tables
[WHERE conditions];
```

평균을 구하는데 사용한다. 

- NULL 값을 제거한 뒤에 평균을 구하기 위해서는?

### 1.4 MAX - 최댓값 구하기

```sql
SELECT MAX(aggregate_expression)
FROM talbes
[WHERE conditions];
```

### 1.5 MIN - 최솟값 구하기

```sql
SELECT MIN(aggregate_expression)
FROM talbes
[WHERE conditions];
```

### 1.6 GROUP BY - 그룹화

```sql
SELECT expression1, expression2, ...expression_n,
       aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
[ORDER BY expression [ ASC | DESC ]];
```

그룹화란 데이터를 그룹 단위로 묶어 집계함수를 적용하는 방법이다. 특정 기준에 따라 데이터를 분류하고, 그룹별로 계산 결과를 얻을 수 있다.

예를들어 점포별, 상품별, 월별, 일별 등 기준에 따라 집계할 때 사용한다.

만약 GROUP BY에 지정한 열 이외에 열을 SELECT 구에 지정하면 에러가 발생한다. 집계함수는 그룹당 하나의 행을 반환하다. 하지만 이외에 열을 지정하면 데이터베이스는 혼란스럽다. 따라서 에러가 발생한다.

**Q. 중복을 제거하는 DISTINCT와 같은거 아닌가요?**
 
두 가지 방법 모두 중복을 제거하는데 사용할 수 있지만 GROUP BY 절은 집계함수와 함께 사용한다.

### 1.7 HAVING - 조건 지정

```sql
SELECT expression1, expression2, ... expression_n,
    aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
HAVING condition
```

그룹화된 데이터의 조건을 지정할 때 사용한다. 앞서 배운 WHERE 절은 개별 레코드에 필터링을 수행하는 반면, HAVING 절은 그룹화된 데이터를 필터링 한다.

WHERE 절과 비슷한 방법으로 사용가능하지만 HAVING 절은 집계함수와 함께 사용한다.

> **내부처리 순서**
> 
> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY

### 함께 사용하는 함수

**1. DISTINCT[^1]**: 중복 값을 제거하는 함수, NULL 값을 무시하지 않는다.

```sql
SELECT DISTINCT expressions
FROM tables
[WHERE conditions];
```

### 집계함수와 함께 춤을

예제와 실제 사용사례, 문제

## 2. 서브쿼리(Subquery)

- 서브쿼리 정의
- 서브쿼리 사용방법
- 서브쿼리 패턴(하나의 값, 복수의 행이지만 열은 하나, 하나의 행이 반환되지만 열이 복수, 복수의 행, 복수의 열 반환)
- IN, NOT IN

서브쿼리란 쿼리안에 또 다른 쿼리를 선언하는 방법을 의미한다. 서브쿼리는 WHERE, FROM, SELECT 절 등 어느절에서든 사용가능하다. 특히 WHERE 절에서 주로 사용한다.

서브쿼리를 사용하면 조금 더 복잡한 쿼리를 정의할 수 있다. 복잡한 쿼리란 다양한 문제를 해결할 수 기회가 주어진다고 생각해도 좋다. 서브쿼리는 한번에 이해하기 힘들다. 한번에 정의하려고 하기보단,
여러번 나눠서 걸쳐 작성해도 좋으니 어떻게 하나로 합칠 수 있을까?를 고민하자.

서브쿼리는 중첩쿼리(nested query), inner query라고도 한다. outer query(main query): 서브쿼리를 포함하는 쿼리, 서브쿼리는 ()안에 정의한다.

- unqualified attribute
- 안쪽 쿼리는 무조건 SELECT로 정의한다.

서브쿼리를 먼저 실행하고, DELETE 명령을 실행한다.

### 스칼라(Scalar)

'스칼라 값'이란 '단일 값'을 반환하는 서브쿼리를 의미한다. 스칼라 값을 다른 서브쿼리 패턴들 중 사용하기 쉬운 장점을 가진다.

## 상관 서브쿼리

**<SQL전문가 정미나>**

- SELECT: 스칼라 서브쿼리
- FROM: 인라인 뷰
- WHERE: 중첩 서브쿼리

**<데이터리안>**

- WHERE 서브쿼리: `=`은 결과물이 1개, IN은 여러개 중 하나


## 마치며

책을 읽을 때마다 몰랐던 수학용어를 마주할 수 있어서 반갑다. 예를 들어 최근에 파라미터가 그렇듯이 이번에는 서브쿼리 중 스칼라에 대해 배울 수 있어서 재밌었다. (사용하면서 전혀 수학용어라고 생각하지 못했다.)

이번장은 특히 이전에 집계함수와 그룹화를 이해하지 못해서 쿼리작성 시 동일한 오류를 마주했던 경험이 있어 더욱 주의 깊게 살펴보고 정리했다.

채용공고에서 자주 이야기하는 개념 중 서브쿼리가 있는데, 개념 외에 실제 사용하면서 얻는 인사이트와 접목이 필요하다. 기존에 풀었던 문제를 서브쿼리로 개선할 수 없을지 고민해 보자.

**<참고자료>**

1. 『SQL 첫걸음』(아사이 아츠시, 한빛미디어, 2015)
2. [TechOnTheNet 'SQL Tutorial'](https://www.techonthenet.com/index.php)
3. [위키독스 'AI가 알려주는 SQL - 아직 AI가 알아서 못하는 DB 관리'](https://wikidocs.net/book/13790)

[^1]: 별개의, 구별되는
