---
title: 'macOS에서 스프링 부트 개발 환경 구성하기(feat. SDKMAN, Liberica JDK 21)'
date: '2026-04-04T18:13:14+09:00'
categories: ["개발환경"]
tags: ["spring-boot", "macos", "sdkman", "liberica-jdk", "wsl2", "docker", "intellij", "gradle", "onboarding-guide"]
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

Windows는 NT 커널 기반 운영체제다. 서버 개발 생태계는 오랫동안 Linux/Unix 환경을 표준으로 사용했다. `bash`, `grep`, `curl` 같은
유닉스(Unix) 표준 도구가 기본으로 제공되지 않고, 파일 경로 구분자도 `\`(백슬래시)로 리눅스(Linux)의 `/`와 충돌한다.
[WSL2](https://learn.microsoft.com/en-us/windows/wsl/install)는 실제 Linux 커널을 경량 VM 위에서 실행하여 문제를 해결한다.

macOS는 Darwin 커널 기반으로 BSD 유닉스에서 파생된 POSIX 호환 운영체제다. 
터미널을 열면 곧바로 리눅스와 거의 동일한 환경이 구성되어 별도의 리눅스 레이어가 필요하지 않다. 

## 2. Docker Desktop

```shell
brew install --cask docker
```

Windows에서 Docker는 리눅스 커널 기능에 의존하여 WSL2 위에서 동작한다. 
macOS는 Docker Desktop이 내부 VM을 자동으로 처리하는 덕분에 별도 설정 없이 바로 사용 가능하다.

> [OrbStack](https://orbstack.dev/)은 Docker Desktop 대비 메모리 사용량이 현저히 낮아 최근 macOS 사용자 사이에서 주목받고 있다.

## 3. JDK 21

JDK를 설치하는 방법은 다양하다. 공식 사이트에서 직접 다운로드, Homebrew, IntelliJ IDEA를 통해 설치할 수 있다. 
하지만 실제 개발환경은 프로젝트마다 JDK 버전이 다른 상황이 자주 발생한다. 
예를 들어 레거시 프로젝트는 Java 8, 새로운 프로젝트는 JDK 21을 사용하는 경우다.

[SDKMAN](https://sdkman.io/)[^1]은 이 문제를 깔끔하게 해결한다.

- 여러 JDK 버전을 설치하고 간단한 명령어로 전환
- Gradle, Maven, Spring Boot CLI 등 JVM 생태계 도구를 함께 관리
- `.sdkmanrc` 파일로 프로젝트별 버전을 고정하여 팀원과 환경 통일 가능

### 3.1 설치

**SDKMAN 설치**

```shell
curl -s "https://get.sdkman.io" | bash
```

**Liberica JDK 21 설치**

> JDK 배포판은 Spring 공식 문서에서 추천하는 Liberica를 선택했다.

```shell
# 설치 가능한 Liberica 버전 확인
sdk list java | grep librca

# Liberica JDK 21 LTS 설치
sdk install java 21.0.7-librca

# 설치 확인
java -version
```

**프로젝트별 버전 고정**

```shell
sdk env init
```

프로젝트 루트에서 `sdk env init`을 실행하면 `.sdkmanrc` 파일을 생성한다.

```shell
# .sdkmanrc
java=21.0.7-librca
gradle=8.13
```

이후 프로젝트 디렉터리에서 `sdk env`를 실행하면 지정한 버전으로 전환한다.

## 4. Gradle

```shell
./gradlew build
./gradlew bootRun
```

Spring Initializr로 생성한 프로젝트는 Gradle Wrapper(`./gradlew`)가 기본으로 포함된다. 
Wrapper는 프로젝트가 요구하는 Gradle 버전으로 자동으로 내려받아 실행하기 때문에, 
전역 Gradle 설치 없이도 팀 전체가 동일한 버전으로 빌드할 수 있다.

```shell
sdk install gradle
```

전역 설치가 따로 필요한 경우 SDKMAN으로 설치한다.

## 5. IntelliJ IDEA

[JetBrains 공식 사이트에서 다운로드](https://www.jetbrains.com/idea/download/?section=mac) 할 때 Apple Silicon 버전을 선택한다.
Intel 버전을 설치하면 Rosetta 2를 통해 동작하여 성능 차이가 발생할 수 있다.

> SDKMAN으로 설치한 JDK는 `~/.sdkman/candidates/java/current`에 위치한다. IntelliJ에서 SDK를 찾지 못하면 경로를 직접 지정한다.

## 마치며

| 도구 | Windows(책 기준) | macOS |
|---|---|---|
| Linux 환경 | WSL2(Ubuntu 24.04) | 불필요 (Unix 기반) |
| JDK 21 | SDKMAN | SDKMAN + Liberica 21 LTS |
| Gradle | SDKMAN | Gradle Wrapper(`./gradlew`) |
| IntelliJ IDEA | Windows 버전 | Apple Silicon 버전 |
| Docker Desktop | WSL2 연동 | macOS용 직접 설치 |

### 참고 자료

- [『스프링 부트 개발자 온보딩 가이드: 스프링 부트로 시작하는 첫 실무 프로젝트』(박상현, 한빛미디어, 2025)](https://product.kyobobook.co.kr/detail/S000218674714)
- [SDKMAN 'Liberica (Bellsoft)'](https://sdkman.io/jdks/librca/)

[^1]: SDKMAN(The Software Development Kit Manager)는 JVM 생태계 SDK 전문 버전 관리 도구다. 2012년부터 개발되어 Java 개발자 사이에 거의 표준으로 사용되어 왔다.
