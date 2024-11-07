---
title: "계층화 아키텍처(Layered Architecture)"
description: ""
date: 2024-10-22 20:42:58
update: 2024-10-22 20:42:58
tags:
  - 스터디
  - 인프런
  - 인프런워밍업클럽
  - 스터디2기
series: "인프런 워밍업 클럽 스터디 2기 - 백엔드 클린 코드, 테스트 코드" 
---

![인프런 워밍업 클럽 스터디 2기 - 백엔드 클린 코드, 테스트 코드 <출처: 인프런>](../images/inflearn-warmup-club-study-2.png)

> *인프런 워밍업 클럽 2기, 18일차 미션을 '나만의 언어'로 정리한 글이다.

## 1. Presentation Layer

**'화면에 정보 표현하기'가 주관심사다.** 외부 세계와 상호작용하는 영역이다.
비즈니스 로직에 관심 두지 않는다. `View`, `Controller`가 해당된다.

## 2. Business Layer

**트랜잭션, 도메인 간 순서를 보장한다.** 화면을 어떻게 출력할지, 데이터를 어떻게 가져오는지에 대해 관심 가지지 않는다.
Persistence Layer에서 데이터를 가져와 로직을 수행하고 결과를 Presentation Layer에 전달한다.

- `@Transaction`을 사용한다.

### 3. Domain Layer

**비즈니스 로직을 처리한다.**

## 4. Persistence Layer

**데이터 저장소에 접근한다.** `Repository`, `DAO`가 해당된다.

## 테스트는 어떻게 작성해야 할까?

- 테스트를 작성할 때 'ORM에서 기본적으로 제공하는 메서드'는 테스트를 작성하지 않는다.
- 의존성 주입을 사용한다.
- Mocking을 통해 단위 테스트를 작성한다.
- 통합 테스트를 작성한다.
