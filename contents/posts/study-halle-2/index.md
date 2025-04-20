---
title: "데이터 타입, 변수 그리고 배열"
description: ""
date: 2025-04-19 23:46:08
update: 2025-04-19 23:46:08
tags:
  - Java/Kotlin
series: "스터디 할래? 온라인 자바 스터디"
---

## 목표

- 기본형 변수와 배열 사용법
- primitive type 종류와 값의 범위 그리고 기본 값
- literal
- 변수 선언및 초기화하는 방법
- 변수의 스코프와 라이프타임
- 타입 변환, 캐스팅 그리고 타입 프로모션
- 1차 및 2차 배열 선언하기
- 타입 추론, var

## 기본형 변수와 배열 사용법

### Java

```java
int balance = 10000;
int[] numbers = {1, 2, 3, 4, 5, 6};
```

기본형(Primitive Type)은 `int`, `long`, `double`, `boolean`처럼 값을 변수에 직접 대입한다.

### Kotlin

```kotlin
val balance: Int = 10000
val numbers = arrayOf(1, 2, 3, 4, 5, 6)
```

Kotlin은 모든 타입을 객체로 취급한다. 하지만 내부적으로 Java의 기본형으로 처리한다.

## 기본형 종류와 값의 범위 그리고 기본값

## 마치며 

