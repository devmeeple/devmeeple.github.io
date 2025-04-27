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
- instanceof
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자

## 산술 연산자(Arithmetic Operators)

산술 연산은 Java와 동일하다.

```kotlin
val x = 10
val y = 5

println(a + b)
println(a - b)
println(a * b)
println(a / b)
println(a % b)
```

## 비트 연산자(Bitwise Operators)

- `shl`
- `shr`
- `ushr`
- `and`
- `or`
- `xor`
- `inv()`

Kotlin은 Java의 `&&`, `||`, `!` 연산자 대신 함수를 사용한다.

## 마치며 

### 참고 자료

- [Baeldung 'Using Bitwise Operators in Kotlin'](https://www.baeldung.com/kotlin/bitwise-operators) 
