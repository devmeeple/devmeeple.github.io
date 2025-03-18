---
title: "E13: 필라멘트"
description: ""
date: 2025-03-17 04:30:00
update: 2025-03-17 22:00:00
tags:
  - 회고/일간
  - 랩/힙합
series: "일간 장태근" 
---

![넉살 '필라멘트 (Feat. BSK A.K.A 김범수)'](20115642.jpg)

언젠가 빛을 다하고 끊어질까

## 1. Permanent Note

### 1.1 Kotlin in Action

- **컬렉션을 다룹니다. 그런데 함수형을 곁들인**
    - 컬렉션을 다룰 때, 표준 라이브러리와 람다를 조합하면 우아한 코드가 만들어진다.
    - 일반적인 연산을 일관성 있게 표현한다.
    - 적은 콘텍스트를 공유하여 인지비용을 낮춘다.
- **시퀀스: 컬렉션 연산 지연 후 실행하기**
    - 즉시 실행과 지연 실행, 적재적소에 활용하기

> filter, map, reduce, fold

- 람다를 인자로 받은 함수에 람다를 넘기면 불필요한 계산이 발생할 수 있다. 작성한 코드가 어떤 결과를 불러올지 명확히 이해해야 한다.
- `reduce`: 첫 번째 값이 누적기(accumulator)에 전달된다.
- `fold`: 초깃값을 선택한다.
- `find` vs. `firstOrNull`
- `associate`
- `replaceAll` vs. `fill`

### 1.2 만화로 배우는 리눅스 시스템 관리

- System Admin Girl, 이 세계에서는 내가 시스템 관리자?
- `SSH(Secure SHell)`, 암호화를 곁들인 원격 접속
    - 안전하지 않은 쉘 `RSH(Remote SHell)`
- `root`, 모든 힘을 갖고 있는 절대 관리자.
    - `sudo`를 통해 권한을 위임한다. (암행어사)
- `grep(Global Regular Expression Print)`, 정규표현식을 통해 문자열 검색
- `vim`
    - 서버는 최소한의 서버를 구성하기 위해 '데스크톱 환경'을 구축하지 않는다.
    - `vim`은 `vi`의 업그레이드다. PC가 대중화되기 이전, 하나의 키가 여러 역할을 하도록 설계했다.
    - `i`: 편집 모드
    - `:wq`: 쓰기 종료
    - `esc`: 일반 모드
    - `/`: 일반 모드 검색
        - `N`: 다음 검색 결과로 이동
        - `Shift` + `N`: 이전 검색 결과로 이동

### 1.3 자바 알고리즘 인터뷰 with 코틀린

> 코딩 테스트 준비 그 이상을 향해.

- 알고리즘은 취업에만 유용할까? 스프링 기술을 잘 이해하기 위해서는 스프링 각 기술에 적용된 알고리즘을 이해해야 한다. 알고리즘이 사용되지 않는 곳이 없다.
    - `DispatcherServlet`
    - `DI(Dependency Injection)`
    - `DataSource`
- 스프링을 사용하는 개발자는 매일 알고리즘을 설계하고 조합하여 서비스를 제공한다 해도 과언이 아니다.
- **자료구조의 특징을 이해하고 적절한 활용이 중요하다.**
    - 시간 복잡도 제대로 계산하는 방법
- **직접 풀고 풀이와 비교하기, 코드 품질과 최적화 기법 익히기**
- 인텔리제이는 2001년에 출시됐다.

## 2. Literature Note

### 2.1 LeetCode

- [(LC-Replied) New kotlin version](https://leetcode.com/discuss/post/1251018/lc-replied-new-kotlin-version-by-kevlar_-wtx5/):
  현재, 코틀린 `1.9.0`를 지원한다.

## 마치며

- 리듬을 바꾸고 있다.
- 책을 주로 읽었더니 강의 영상이 낯설어 고민이다.
