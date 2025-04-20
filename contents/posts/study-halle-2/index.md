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

기본형, 변수와 배열을 사용하는 방법을 학습한다.

- 타입 추론, var

## 기본형 변수와 배열 사용법

**Java**

```java
int balance = 10000;
int[] numbers = {1, 2, 3, 4, 5, 6};
```

기본형(Primitive Type)은 `int`, `long`, `double`, `boolean`처럼 값을 변수에 직접 대입한다.

**Kotlin**

```kotlin
val balance: Int = 10000
val numbers = arrayOf(1, 2, 3, 4, 5, 6)
```

Kotlin은 모든 타입을 객체로 취급한다. 하지만 내부적으로 Java의 기본형으로 처리한다.

## 기본형 종류와 값의 범위 그리고 기본값

Java와 Kotlin 모두 동일한 범위를 갖는다. 하지만 Kotlin은 기본값이 없기 때문에 명시적으로 초기화해야 한다.

## 리터럴(Literal)

개발자가 직접 입력한 고정된 값을 의미한다.

## 변수 선언 및 초기화하는 방법

변수 선언은 컴퓨터 메모리 공간을 확보하고 데이터를 저장한다. 변수의 이름, 식별자를 통해 메모리 공간에 접근한다. 

**Java**

```java
int amount = 12900;
```

**Kotlin**

```kotlin
// 읽기 전용 변수 (변경 불가능)
val number: Int = 10

// 변경 가능한 변수
var amount = 12900 
amount = 13000
```

## 변수의 스코프와 라이프 타임

```kotlin
fun main() {
    val x = 10
    if (true) {
        val y = 20
        println("x의 값: $x") // 10
        println("y의 값: $y") // 20
    } // y 라이프 타임 종료
} // x 라이프 타임 종료
```

**스코프(Scope)란 접근 가능한 범위를 의미한다.** 지역 변수는 선언된 코드 블록 안에서만 접근 가능하다. 코드 블록을 벗어나면 접근할 수 없다. 스코프를 통해 필요한 곳에서만 접근할 수 있는 한정된 코드를 작성하자.

## 자동 형변환과 명시적 형변환

**Java**

작은 범위 숫자 타입에서 큰 범위 숫자 타입으로 값을 대입할 때 개발자는 직접 형변환 하지 않아도 된다. 자동으로 일어나기 때문에 자동 형변환(Promotion) 또는 묵시적 형변환이라 한다.

서로 다른 타입을 계산할 때 큰 범위로 자동 형변환이 일어난다.

```java
double doubleValue = 1.8;
int intValue = (int) doubleValue; // 1
```

큰 범위 숫자 타입에서 작은 범위 숫자 타입으로 값을 대입할 때 개발자가 직접 형변환 코드를 입력한다. 이를 명시적 형변환(Casting)이라 한다. 소수점이 버려지고 오버플로(Overflow)를 유의해야 한다.

**Kotlin**

```kotlin
val intValue = 10
val longValue = intValue.toLong()
```

Kotlin은 자동 형변환이 일어나지 않는다. 명시적으로 변환 함수를 호출한다.

## 배열 선언하기

**Java**

```java
// 1차원 배열
int[] array = new int[3];
int[] numbers = {1, 2, 3};

// 2차원 배열
int[][] matrix = new int[2][3]; 
```

**Kotlin**

```kotlin
// 1차원 배열
val array = IntArray(3)
val numbers = arrayOf(1, 2, 3)

// 2차원 배열
val matrix = Array(2) { IntArray(3) }
```

## 마치며 
