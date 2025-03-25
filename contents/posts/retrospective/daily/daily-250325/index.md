---
title: "2025-03-25: 살기 위해서"
description: ""
date: 2025-03-25 03:00:00
update: 2025-03-25 22:00:00
tags:
  - 회고/일간
series: "일간 장태근" 
---

## 컴퓨터 밑바닥의 비밀

> 1장, 프로그래밍 언어부터 프로그램 실행까지, 이렇게 진행된다

### 컴파일러는 번역가다

우리의 기록은 `소스 파일(source file)`이다. `컴파일러`는 `소스 파일`을 `CPU`가 실행할 수 있도록 `실행 파일`로 변환한다.

### 토큰은 최소 단위다

컴파일러는 소스 코드에서 `토큰(token)`을 추출한다. 추출하는 과정을 `어휘 분석(lexical analysis)`이라고 한다.

### 링커는 예언자다

소스 파일은 `대상 파일(object file)`이 존재한다. 대상 파일과 소스 파일을 병합하기 위해 `링커(linker)`를 사용한다. 링커는 압축 프로그램처럼 소스 파일과 대상 파일을 묶어 하나의 실행 파일을
만든다. 링커는 전역 변수, 외부 모듈 같은 참조할 수 있는 대상에 관심을 둔다.

### 톺아보기: 자바와 링커

- 자바도 컴파일이 필요하다. 하지만 이전에 배운 전통적 방식[^1]과 다른 방식을 채택했다. 목적파일을 연결하고 실행 파일을 만들지 않는다.
- `클래스 로더(Class Loader)`, 자바는 클래스 로딩, 링킹, 초기화가 모두 '프로그램 실행 중(Runtime)'에 동적으로 이뤄진다.
- `WORA(Write Once, Run Anywhere)`, 하드웨어 플랫폼에 종속되는 구조를 탈피했다.
- 링킹은 `검증(verification) -> `준비(preparation) -> 해석(resolution)` 단계로 이뤄진다.

**<참고 자료>**

- [『JVM 밑바닥까지 파헤치기』(저우즈밍, 인사이트, 2024)](https://product.kyobobook.co.kr/detail/S000213057051)
- [Stack Overflow 'How Java linker works?'](https://stackoverflow.com/questions/6440310/how-java-linker-works)

## 자바 알고리즘 인터뷰 with 코틀린

### 1. 제네릭: 안전한 코드 작성하기

`컴파일 타임(Compile Time)`에 클래스나 메서드에 사용할 자료형을 지정하여 타입 검사에 도움을 받는다.

### 2. 함수형 프로그래밍 언어

- 람다 표현식
- 스트림 API

`Java 8` 이전에는 객체 지향 외에 절차 지향, 함수형 프로그래밍 개념을 배척하다 싶은 행보를 보냈다. `OOP`를 코딩 테스트에서 활용하기란 어렵다. 하지만 함수형은 코딩 테스트에 매우 유용하다.

## 마치며

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/4UasKCFGJCnCchh3UrpV58?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
