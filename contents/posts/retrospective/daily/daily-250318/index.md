---
title: "E14: Kaze"
description: ""
date: 2025-03-18 04:30:00
update: 2025-03-18 17:00:00
tags:
  - 일간
series: "일간 장태근" 
---

![]()

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

## 2. Literature Note

## 마치며 

