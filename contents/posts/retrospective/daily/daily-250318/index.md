---
title: "E14: 바람"
description: ""
date: 2025-03-18 04:30:00
update: 2025-03-18 17:00:00
tags:
  - 회고/일간
  - Kotlin/코틀린
  - 발라드
series: "일간 장태근" 
---

![윤하 '바람'](4086334.jpg)

아무도 만질 수 없는 기억의 바람

## 1. Permanent Note

### 1.1 Kotlin in Action

> 7. 널이 될 수 있는 값

- **nullable type**
    - 최신 언어들은 실행 환경이 아닌 아닌 컴파일 단계에서 `NPE(NullPointerException)`가 발생할 수 있도록 지원한다.
- 타입 뒤에 `?`는 해당 타입이 널을 참조할 수 있음을 암시한다.
- 널이 될 수 있는 타입과, 널이 될 수 없는 타입을 구분하면 어떤 연산이 가능한지 명확하게 이해할 수 있다.
    - 실행 환경은 같은 타입이다. 래퍼 타입이 아니다.
- **null을 다루는 방법**
    - `if`
    - `?.`
        - 호출 값이 `null`이 아니면 일반 메서드 호출처럼 동작한다.
        - 호출 값이 `null`이라면 호출을 무시한다.
    - `?:`
        - `null`을 특정 값으로 변경한다. 기본값 할당에 주로 사용한다.
    - `안전한 캐스트 연산자(safe-cast operator)`
    - `!!(not-null assertion)`
        - 컴파일러에게 `null`이 아님을 단언한다.
        - `null`이면 `NPE`가 발생한다.
        - 다른 방법을 우선 고려하자.
    - `let 함수`
    - `lateinit`
    - `DI(Dependency Injection`를 적용한 프레임워크 사례

### 1.2 자바 알고리즘 인터뷰 with 코틀린

> 플랫폼 별 특징과 활용, 사전 준비

- 코딩 인터뷰는 마이크로소프트가 처음 도입한 것으로 추정된다. 꾸준히 확대되어 컴퓨터 과학 기본기 검증에 주로 사용한다.
- 면접관이 함께하는 방식을 '인터뷰'로 분류하고, 시험을 치르는 방식을 '테스트'로 분류한다.
- **온라인 코딩 테스트의 사전 준비 사항**
    - 연습장과 필기 도구: 값의 변화, 최종 결과를 기록하고 풀이를 비교한다.
    - 나만의 코드 스니펫(Snippet)
    - 예외 처리
    - REPL(Read Evaluate Print Loop) 도구로 코드 검증
    - 코딩 테스트 플랫폼 숙지: 해커랭크, 프로그래머스

## 2. Literature Note

- [『우주비행사의 지구생활 안내서』(크리스 해드필드, 더퀘스트, 2014)](https://product.kyobobook.co.kr/detail/S000001031978)
    - Chris Hadfield
- [GeekNews '새로운 출발을 준비할 때 읽어볼 100권의 책'](https://news.hada.io/topic?id=19809&v2)
- [GeekNews 'HTTP/3가 널리 지원되지만 실제로는 거의 사용되지 않는 이유'](https://news.hada.io/topic?id=19816)
- [Kotlin Docs 'Nullability in Java and Kotlin﻿'](https://kotlinlang.org/docs/java-to-kotlin-nullability-guide.html#support-for-definitely-non-nullable-types)
- [Kotlin Docs 'Null safety'](https://kotlinlang.org/docs/null-safety.html)
- Predicate: 주어진 조건 만족 여부를 검증하는 함수나 표현식
- Precondition: 사전 조건

## 마치며 

