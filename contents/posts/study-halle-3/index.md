---
title: "연산자"
description: ""
date: 2025-04-27 17:00:00
update: 2025-04-27 18:00:00
tags:
  - Java/Kotlin
series: 
---

- 관계 연산자
- 논리 연산자
- is 연산자
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자

## 산술 연산자(Arithmetic Operators)

산술 연산자는 Java와 동일하다.

```kotlin
val x = 10
val y = 3

println(a + b)
println(a - b)
println(a * b)
println(a / b)
println(a % b)
println(x / y.toDouble())
```

두 정수의 나눗셈 연산 결과는 정수다. 소수점을 얻고 싶다면 최소 한쪽을 실수로 변환해야 한다.

## 비트 연산자(Bitwise Operators)

```kotlin
val x = 0b1100 // 12
val y = 0b1010 // 10

println(x and y)   // AND
println(x or y)    // OR
println(x xor y)   // XOR
println(x shl 2)   // 좌측 시프트
println(x shr 2)   // 우측 시프트
println(x ushr 2)  // 부호 없는 우측 시프트
```

Kotlin은 Java의 `&&`, `||`, `!` 연산자 대신 명확한 함수를 사용한다.

## is 연산자

Java의 instanceOf

## when 표현식

Kotlin은 Java의 개선된 `switch`문 처럼 `when` 표현식을 제공한다.

```kotlin
val day = 5
val dayOfWeek = when (day) {
    1 -> "월요일"
    2 -> "화요일"
    3 -> "수요일"
    4 -> "목요일"
    5 -> "금요일"
    6, 7 -> "주말"
    else -> throw IllegalArgumentException("1부터 7까지 숫자 중 입력해주세요")
}
```

## 마치며 

### 참고 자료

- [Baeldung 'Using Bitwise Operators in Kotlin'](https://www.baeldung.com/kotlin/bitwise-operators) 
