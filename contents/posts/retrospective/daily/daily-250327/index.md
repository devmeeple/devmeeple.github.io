---
title: "2025-03-27 HOT"
description: ""
date: 2025-03-27 22:53:33
update: 2025-03-27 22:53:33
tags:
  - 회고/일간
  - Kotlin/코틀린
  - CS
  - Design Pattern/디자인 패턴
series: "일간 장태근" 
---

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/406IpEtZPvbxApWTGM3twY?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

- 노동요, 내가 나로 살 수 있다면, 재가 된대도 난 좋아

## 1. Java to Kotlin

### 1. 당신의 엔티티는 안전하십니까

> 1. `엔티티`는 `JPA의 엔티티(@Entity)`와 1:1 대응될까?
> 2. `JPA`가 없으면 `엔티티`는 허상인가?

- 추상적이고 보편적인 엔티티를 구체화한 결과가 `JPA 엔티티`라고 생각한다.
- 문맥에 따라 다르지만, 주로 사용하는 엔티티는 도메인 엔티티(비즈니스 객체)를 의미한다.
- `JPA 엔티티`의 뿌리는 `DB 엔티티`에 가깝다. 추상적인 엔티티를 구현 기술(JPA)에 맞춰 구체화한 결과물이다.
- **따라서, `JPA 엔티티`는 `영속성 객체(PO: persistent object)`[^1]다.**

## 마치며

### 오늘의 함께 읽기

> [얄팍한 코딩사전 '01. 파사드(Facade) 패턴'](https://www.youtube.com/watch?v=FrdG_n2ZWtE&t=113s)

- `퍼사드 패턴(Facade Pattern)`, 소통 창구를 열어 클라이언트와 소통한다. 구조패턴에 속한다.
- `Spring`은 어떻게 활용하고 있을까?

[^1]: 데이터가 영원히 이어지도록 임의의 공간에 저장하고 불러온다.
