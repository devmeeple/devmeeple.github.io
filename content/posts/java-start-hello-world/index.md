---
title: 'Hello World'
date: '2026-03-07T22:20:58+09:00'
categories: ["Java"]
tags: []
series: ["Java에서 살아남기"]
series_order: 1
draft: true
---

- 자바란?
  - 표준스펙과 구현, JCP
- 개발 환경 설정
  - IntelliJ(Toolbox)
  - VSCode
- 자바 설치(IntelliJ를 사용할 때와 직접 설치할 때의 차이), JDK, JRE
- 질문
  - 어떤 JDK를 사용하면 좋을까?

## JDK vs. JRE

- Java 애플리케이션 개발을 위해서는 JDK가 필요하다.
- JDK(Java Development Kit)는 Java를 애플리케이션을 개발하는데 필요한 모든 요소(컴파일, 패키징, 실행 등)를 포함한다. 
- JRE(Java Runtime Environment)는 JDK의 축약 버전이다. 애플리케이션을 실행하는데 필요한 요소만 포함한다.

## Java를 설치하는 방법

### IntelliJ에서 설치

- 프로젝트를 생성, 설정할 때 필요한 JDK를 쉽게 설치할 수 있다.
- IntelliJ 내부에서만 JDK를 사용한다. 따라서 시스템 전역 환경변수 등록이 필요하다.

### 직접 설치

- IntelliJ 뿐만 아니라 다양한 환경에서 Java를 사용할 수 있다.
- [mise](https://mise.jdx.dev/)는 다양한 개발환경을 관리하는 도구다.

## 마치며

### 참고 자료

- [Which Version of JDK Should I Use?](https://whichjdk.com/)
