---
title: "IntelliJ IDEA 가이드"
description: ""
date: 2025-11-09 09:00:00
update: 2025-11-09 18:00:00
tags:
  - IDE
series: 
---

- 주로 사용하는 단축키를 macOS 기준으로 정리했다.

## 코드 수정

### 메인 메서드 생성 및 실행

- 파일, 디렉터리, 클래스 추가: `Command` + `N`
    - 현재 위치에 따라 생성 가능한 항목 목록 표시
- 계층 구조 작성
    - 디렉터리: `/` (예: `src/main/java`)
    - 패키지: `.` (예: `io.github.devmeeple`)
- 자주 사용하는 코드 구문은 [Live templates](https://www.jetbrains.com/help/idea/using-live-templates.html)에 기본 정의되어 있음
    - `psvm` -> `public static void main(String[] args)`
    - `sout` -> `System.out.println()`
- 메인 메서드 실행: `Ctrl` + `Shift` + `R`
- 최근 실행 환경 재실행: `Ctrl` + `R`

### 라인 수정하기

- 한 줄 복사: `Command` + `D`
- 한 줄 삭제: `Command` + `Backspace`
- 라인 합치기(병합): `Ctrl` + `Shift` + `J`
    - 포커스 위치와 관계없이 줄 단위로 합침
- 라인 이동
    - 코드 구조에 따라 이동: `Command` + `Shift` + `↑/↓`
    - 단순 라인 이동(구문 무시): `Option` + `Shift` + `↑/↓`
        - Markdown 문서에 유용
- 요소(Element) 이동: `Command` + `Option` + `Shift` + `←/→`
    - HTML 등 태그 단위 이동시 사용

### 코드 즉시보기

- 메서드 인자 정보 보기: `Command` + `P`
- 구현부 빠르게 확인: `Option` + `Space`
- API 문서 보기: `F1`

## 포커스

### 포커스 에디터

- 단어 단위 이동: `Option` + `←/→`
- 단어 단위 선택: `Option` + `Shift` + `←/→`
- 라인 처음/끝으로 이동: `Command` + `←/→`
- 라인 전체 선택: `Command` + `Shift` + `←/→`

### 포커스 특수키

- 포커스 범위 확장/축소: `Option` + `↑/↓`
- 이전/다음 포커스 위치로 이동: `Command` + `[` / `Command` + `]`
- 멀티 포커스(여러 커서 추가): `Option` + `Option` + `↑/↓`
- 오류 라인으로 자동 포커스 이동: `F2`

## 검색

### 텍스트

- 검색
    - 현재 파일: `Command` + `F`
    - 프로젝트 전체: `Command` + `Shift` + `F`
- 교체
    - 현재 파일: `Command` + `R`
    - 프로젝트 전체: `Command` + `Shift` + `R`
- 참고: 정규 표현식(Regular Expression)을 함께 사용하면 검색과 교체를 더욱 효율적으로 수행 가능

### 기타 검색

- 전체 검색(모든 항목 접근): `Shift` + `Shift`
    - 파일, 메서드, 액션 등 한 번에 탐색 가능
- 파일 검색: `Command` + `Shift` + `O`
- 메서드 검색: `Command` + `Option` + `O`
- 액션 검색(Actions): `Command` + `Shift` + `A`
- 최근 열었던 파일 목록: `Command` + `E`
    - 최근 수정한 파일 목록: `Command` + `E`를 두번 입력(`Command` + `E`, `Command` + `E`)

## 코드 자동완성

- 스마트 자동완성: `Ctrl` + `Shift` + `Space`
    - 현재 문맥에 맞는 타입의 값만 제안
- 정적 메서드 자동완성: `Ctrl` + `Space`를 두번 입력
    - [AssertJ](https://assertj.github.io/doc/)를 같은 라이브러리 사용 시 특히 유용
- 생성자/Getter/Setter 자동완성: `Command` + `N`
    - `Shift`를 누르면 여러 필드 선택 가능
- Override 메서드 자동 완성: `Ctrl` + `I`

### Live Template

- Live Template 목록 보기: `Command` + `J`
- 사용자 정의 Template 등록 가능
    - 자주 사용하는 코드 구조를 미리 정의해두면 효율적으로 활용 가능
        - 테스트 코드 기본 구조
        - JPA Entity 패키지 스켈레톤

## 리팩터링

### Extract

- 변수 추출: `Command` + `Option` + `V`
- 매개변수 추출: `Command` + `Option` + `P`
- 메서드 추출: `Command` + `Option` + `M`
- 이너클래스 추출: `F6`

### 기타

- 이름 일괄 변경: `Shift` + `F6`
- 타입 일괄 변경: `Command` + `Shift` + `F6`
- 사용하지 않는 import 정리: `Ctrl` + `Option` + `O`
    - 단축키 대신 추가 설정으로 대체 가능(Optimize imports on the fly)
- 정렬: `Command` + `Option` + `L`

### 마치며

- IntelliJ 사용에 익숙해졌다고 착각했다.
- 생산성을 높여주는 수많은 기능이 숨겨져 있었다. 덕분에 불필요한 작업 시간을 줄이고 코드 작성에 더욱 집중할 수 있게 됐다.

### 참고 자료

- [향로 'IntelliJ를 시작하시는 분들을 위한 IntelliJ 가이드'](https://inf.run/zxA3z)
