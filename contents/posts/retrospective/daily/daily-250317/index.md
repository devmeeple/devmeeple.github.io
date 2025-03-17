---
title: "E13: 오늘의 노래"
description: ""
date: 2025-03-17 04:30:00
update: 2025-03-17 22:00:00
tags:
  - 일간
series: "일간 장태근" 
---

![]()

## 1. Permanent Note

### 1.1 Kotlin in Action

- **컬렉션을 다룹니다. 그런데 함수형을 곁들인**
    - 컬렉션을 다룰 때, 표준 라이브러리와 람다를 조합하면 우아한 코드가 만들어진다.
    - 일반적인 연산을 일관성 있게 표현한다.
    - 적은 컨텍스트를 공유하여 인지비용을 낮춘다.
- **시퀀스: 컬렉션 연산 지연 후 실행하기**
    - 즉시 실행과 지연 실행, 적재적소에 활용하기

> filter, map, reduce, fold

- 람다를 인자로 받은 함수에 람다를 넘기면 불필요한 계산이 발생할 수 있다. 작성한 코드가 어떤 결과를 불러올지 명확히 이해해야 한다.
- `reduce`: 첫번째 값이 누적기(accumulator)에 전달된다.
- `fold`: 초깃값을 선택한다.
- `find` vs. `firstOrNull`
- `associate`
- `replaceAll` vs. `fill`

### 1.2 만화로 배우는 리눅스 시스템 관리

- System Admin Girl, 이세계에서는 내가 시스템 관리자?
- `SSH(Secure SHell)`, 암호화를 곁들인 원격 접속
    - 안전하지 않은 쉘 `RSH(Remote SHell)`
- `root`, 모든 힘을 갖고 있는 절대 관리자.
    - `sudo`를 통해 권한을 위임한다. (암행어사)
- `grep(Global Regular Expression Print)`, 정규표현식을 통해 문자열 검색
- `vim`
    - 서버는 최소한의 서버를구성하기 위해 '데스크톱 환경'을 구축하지 않는다.
    - `vim`은 `vi`의 업그레이드다. PC가 대중화 되기 이전, 하나의 키가 여러 역할을 하도록 설계했다.
    - `i`: 편집 모드
    - `:wq`: 쓰기 종료
    - `esc`: 일반 모드
    - `/`: 일반 모드 검색
        - `N`: 다음 검색 결과로 이동
        - `Shift` + `N`: 이전 검색 결과로 이동

## 2. Literature Note

## 마치며


