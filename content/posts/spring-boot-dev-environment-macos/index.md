---
title: 'macOS에서 스프링 부트 개발 환경 구성하기(feat. SDKMAN, Liberica JDK 21)'
date: '2026-04-04T18:13:14+09:00'
categories: ["Spring"]
tags: ["spring-boot", "sdkman", "liberica-jdk", "wsl2", "docker", "intellij", "onboarding-guide"]
draft: true
---

## 들어가며

『스프링 부트 온보딩 가이드』 1장은 다음 도구로 개발 환경을 정의한다.

- Windows 11
- WSL2(Ubuntu 24.04)
- JDK 21
- Gradle
- IntelliJ IDEA
- Docker Desktop

> macOS 환경에서도 동일하게 구성해야 할까? 대안은 없을까?

Windows 환경에서 도구가 필요한 이유는 무엇이고 macOS 환경에서는 어떤 도구를 선택하면 좋을지 이유를 알아보자.

## 1. WSL2

Windows는 NT 커널 기반 운영체제다. 서버 개발 생태계는 오랫동안 Linux/Unix 환경을 표준으로 사용했다. 따라서 리눅스(Linux) 환경에서 개발하기 위해서 WSL2를 사용한다.

macOS는 Darwin 커널 기반 운영체제다. macOS 자체가 유닉스(Unix), 즉 리눅스와 거의 동일한 환경을 제공하기 때문에 별도의 도구가 필요하지 않는다.

## 2. 도커 데스크탑

## 3. SDKMAN

JDK를 설치하는 방법은 다양하다. 공식 사이트에서 다운, Homebrew, IntelliJ IDEA를 사용할 수 있다. 하지만 실제 개발환경은 프로젝트마다 JDK 버전이 다른 상황이 자주 발생한다. 예를들어 레거시 프로젝트는 Java 8, 새로운 프로젝트는 JDK 21을 사용한다.

[SDKMAN](https://sdkman.io/)[^1]은 이러한 문제를 깔끔하게 해결한다. 
- 여러 JDK 버전을 설치하고 간단한 명령어로 전환
- Gradle, Maven, Spring Boot CLI 등 JVM 생태계 도구도 함께 관리
- `.sdkmanrc` 파일로 프로젝트별 버전을 고정하여 팀원과 환경 통일 가능

### 3.1 설치 과정

**SDKMAN 설치**

```bash
curl -s "https://get.sdkman.io" | bash
```

**Liberica JDK 21 설치**

> JDK는 Spring 공식문서에서 추천하는 Liberica를 선택했다.

```bash
# 설치 가능한 Liberica 버전 확인
sdk list java | grep librca

# Liberica JDK 21 LTS 설치
sdk install java 21.0.7-librca

# 설치 확인
java -version
```

**프로젝트별 버전 고정**

```bash
sdk env init
```

```bash
# .sdkmanrc
java=21.0.7-librca
gralde=8.13
```

이후 프로젝트 디렉터리에서 `sdk env`를 실행하면 지정된 버전으로 전환한다.

```bash
sdk install java 21-tem # JDK 21 설치
sdk use java 21-tem # 현재 shell에서 버전 전환 
sdk default java 21-tem # 전역 기본 버전 설정

sdk install gradle 8.7
```

```bash
# .sdkmanrc (프로젝트 루트에 위치)
java=21-tem
gradle=8.7
```

## 마치며

### 참고 자료

- [『스프링 부트 개발자 온보딩 가이드: 스프링 부트로 시작하는 첫 실무 프로젝트』(박상현, 한빛미디어, 2025)](https://product.kyobobook.co.kr/detail/S000218674714)
- [SDKMAN 'Liberica (Bellsoft)'](https://sdkman.io/jdks/librca/)

[^1]: SDKMAN(The Software Development Kit Manager)는 JVM 생태계 SDK 전문 버전 관리 도구다. 2012년부터 개발되어 Java 개발자 사이에 거의 표준으로 사용되어 왔다.
