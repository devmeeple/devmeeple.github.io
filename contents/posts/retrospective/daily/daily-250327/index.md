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
- [『자바/스프링 개발자를 위한 실용주의 프로그래밍』(김우근, 위키북스, 2024)](https://product.kyobobook.co.kr/detail/S000213447953)

## 2. 컴퓨터 밑바닥의 비밀

> chapter 2, 프로그램이 실행되었지만, 뭐가 뭔지 하나도 모르겠다

- CPU를 우선 다루는 이유는 가장 간단하기 때문이다. 적재된 명령을 선택하고 실행한다. 반복한다.
- CPU는 한 번에 한 가지 일을 수행한다.
- `프로세스(process)`, 얼음땡 마법으로 멀티 태스킹이 가능하다.
- 운영체제, 코드 재사용성의 정수
- 다중 프로세스에서 발생하는 문제

## 3. 자바 알고리즘 인터뷰 with 코틀린

> 3장_코틀린, 구글이 인정한 공식 언어

- 고수준 언어와 저수준 언어는 자동차의 자동, 수동 변속기와 유사하다.
- 자바도 10 버전 이상에서도 타입 추론을 지원한다.

> 117, C++.와 자바에서는 이 기능이 존재하지 않아서 디자인 패턴 중 빌더 패턴(Builder Pattern)이란 것을 고안해 사용해왔는데, 
> 코틀린은 파라미터 이름을 지정할 수 있어서 굳이 빌더 패턴을 사용할 필요가 없으며, 훨씬 더 간단하게 처리할 수 있다. 참고로 이 기능은 파이썬에서도 지원한다.

## 마치며

강철의 연금술사에 홀린 덕분에, 연금술을 부리듯 매일이 즐겁다. 컴퓨터 과학의 마법에 깨달음을 얻고, 이어지는 정리의 순간이 더없이 짜릿하다.

- 강철의 연금술사의 영향인지 연금술을 하고 있는 것 같아 매사가 즐겁다. 정리가 재밌다.

### 오늘의 함께 읽기

> [얄팍한 코딩사전 '01. 파사드(Facade) 패턴'](https://www.youtube.com/watch?v=FrdG_n2ZWtE&t=113s)

- `퍼사드 패턴(Facade Pattern)`, 소통 창구를 열어 클라이언트와 소통한다. 구조패턴에 속한다.
- `Spring`은 어떻게 활용하고 있을까?

[^1]: 데이터가 영원히 이어지도록 임의의 공간에 저장하고 불러온다.
