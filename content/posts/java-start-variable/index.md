---
title: '변수'
date: '2026-03-02T19:32:36+09:00'
categories: ["Java"]
tags: []
series: ["Java에서 살아남기"]
series_order: 2
draft: true
---

## 1. 변수(Variable)

- 변수는 데이터를 간편하게 다루기 위해 메모리 공간에 이름을 부여하는 방법이다.
- 변수가 없는 세상은 서비스에 변경해야 하는 부분이 발생하면 고역을 치렀다. 변경해야 하는 부분을 모두 변경해야 했다. 하지만 변수를 사용하면 임시 공간(메모리)에 데이터(값)를 저장하고 제어한다.
- 변수는 값을 저장하거나(기본형) 객체가 저장된 위치를 참조하는(참조형) 식별자다.
- 지역 변수는 반드시 초기화가 필요하다.

## 2. 변수 시작

- 프로그램은 메모리에 값을 저장하고 꺼내 사용한다.
- 상품이 바코드를 통해 상품의 정보를 식별하듯 변수는 메모리를 참조할 때 사용하는 식별자다.

## 3. 변수 값 변경

```java
String title = "자바의 신";
title = "이펙티브 자바";
```

```text
title = "자바의 신"

Stack:
┌────────────┐
│ title      │ ──▶ "자바의 신"
└────────────┘

title = "이펙티브 자바"

Stack:
┌────────────┐
│ title      │ ──▶ "이펙티브 자바"
└────────────┘
```

- 변수에 새로운 값을 할당하면 이전 값은 사라진다. 변수는 '항상 최신 값'만 갖는다.
- 새로운 값을 할당하기 전 이전 값을 보관하려면 새로운 변수를 선언하고 값을 미리 저장해야 한다.
- 상수는 재할당하지 않아도 되는 고정값에 사용한다. 상수는 특별한 취급을 받는다.

## 4. 변수 선언과 초기화

```java
String title; // 선언
title = "자바의 신"; // 초기화

int price = 30000; // 선언과 초기화를 동시에
```

> [!Caution] 지역 변수는 반드시 초기화 후 사용해야 한다. 따라서 선언과 동시에 초기화를 권장한다.

- 변수 선언은 컴퓨터의 메모리 공간을 사용하겠다는 명령이다.
- 메모리는 여러 프로그램이 함께 사용한다. 변수를 선언하고 초기화하지 않는 행동은 주차 자리 맡기랑 같다. 실제차량(값)이 없으면 사용할 수 없다.
- 지역 변수를 초기화하지 않고 사용하려 하면 컴파일 에러(Compile Error)가 발생하여 프로그램 실행조차 되지 않는다.

## 5. 변수 타입1(기본형)

- 타입은 값이 저장 가능한 범위다. 범위를 벗어나면 에러[^1]가 발생한다.
- 저장 가능한 범위가 크면 메모리도 많이 차지한다.

### 5.1 정수형(Integer)

| 타입 | 크기 | 표현 범위 | 기본값 |
|------|------|------------|--------|
| `byte` | 1 byte (8bit) | -128 ~ 127 | 0 |
| `short` | 2 byte (16bit) | -32,768 ~ 32,767 | 0 |
| `int` | 4 byte (32bit) | -2,147,483,648 ~ 2,147,483,647 | 0 |
| `long` | 8 byte (64bit) | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 | 0L |

### 5.2 실수형(Floating-Point)

| 타입 | 크기 | 표현 범위 (근사값) | 기본값 | 정밀도 |
|------|------|-------------------|--------|--------|
| `float` | 4 byte | ±1.4E-45 ~ ±3.4E38 | 0.0f | 약 7자리 |
| `double` | 8 byte | ±4.9E-324 ~ ±1.8E308 | 0.0d | 약 15자리 |

- 정밀도란 실수형 데이터 타입이 부동소수점 방식으로 소수점을 얼마나 정확하게 표현할 수 있는지 나타내는 지표다. Java에서는 `double`을 주로 사용한다.

### 5.3 문자형(Charater)

| 타입 | 크기 | 표현 범위 | 기본값 |
|------|------|------------|--------|
| `char` | 2 byte (16bit) | 0 ~ 65,535 (Unicode) | `'\u0000'` |

### 5.4 논리형(Boolean)

| 타입 | 크기 | 표현 값 | 기본값 |
|------|------|----------|--------|
| `boolean` | JVM 의존 | `true` / `false` | false |

## 6. 변수 타입2(참조형)

```java
String name = "James Arthur Gosling";
```

- 기본형이 일반 값을 다뤘다면, 참조형은 객체의 주소값을 저장한다.
- 타입에 따라 JVM에 저장되는 위치가 다르다.

## 7. 변수 명명 규칙

- 카멜 케이스(Camel case)를 사용한다.
  - 변수: `camelCase`
  - 클래스: `CamelCase`
- 의도를 전달할 수 있는 명확한 이름을 사용해야 한다.

> [!TIP] [Intellij CamelCase Plugin](https://plugins.jetbrains.com/plugin/7160-camelcase)을 사용하면 쉽게 case를 변경할 수 있다.

## 질문

### Q1. 변수는 언제 사라질까?

```text
JVM 메모리 구조

- Stack: 지역 변수
- Heap: 객체, 인스턴스 변수
- Method Area: 클래스 정보, static 변수
```

- Java의 변수는 선언된 위치와 종류에 따라 소멸 시기가 다르다.
  - 지역 변수(Local Variables): Stack 메모리에 저장, 메서드 실행이 종료되면 Stack에서 즉시 소멸한다.
  - 인스턴스 변수(Instance Variables): Heap 메모리에 저장, 클래스 내에서 선언되며 객체가 생성될 때 만들어진다. 객체를 더 이상 참조하지 않을 때 가비지 컬렉터(GC, Garbage Collection)에 의해 소멸한다.
  - 클래스 변수(Static Variables): Method Area 메모리, `static` 키워드와 함께 선언된다. 클래스가 JVM에 로딩될 때 생성하고, 클래스가 언로드되거나 JVM이 종료되면 소멸한다.

### Q2. String은 왜 특별할까?

- String은 양반집 자식이다.
- String은 자주 사용하는 자료형이지만 기본 자료형(primitive type)이 아니다. 참조형으로 언어의 특별 관리를 받는다.
  - `final` 클래스, 불변성(Immutablility)
  - 메모리 최적화
  - `new` 연산자를 사용하지 않고 문자열 리터럴을 직접 할당할 수 있는 유일 객체

### Q3. 리터럴(Literal)이란 무엇일까?

- '문자 그대로 작성된 값'을 영어로 literal이라 한다.
- 리터럴은 소스 코드에 직접 작성한 값을 의미한다. 컴파일 시점에 이미 결정되어 있다.
- 프로그램 실행 중 생성하는 값은 리터럴이 아니다. 리터럴은 값 자체이며, 변수는 값을 담는 공간이다.

```java
String isbn = "9788966262281" // 9788966262281은 문자열 리터럴이다.
int amount = 0; // 0은 정수형 리터럴이다.
double pi = 3.141592; // 3.141592는 실수형 리터럴이다.
```

## 마치며

- 변수는 값을 저장하거나 객체를 참조하기 위해 메모리 공간에 이름을 붙이는 방법이다. 기본형은 값을 직접 저장하고, 참조형은 객체의 주소를 저장한다.
- 변수의 생명주기는 선언 위치에 따라 다르다.
- 흑백요리사의 대파미션처럼 세상에 변수가 없이 데이터를 다뤄야 했다면 어땠을까. 상상이 안된다.

### 참고 자료

- [인프런 '김영한의 자바 입문 - 코드로 시작하는 자바 첫걸음'](https://inf.run/WUc1V)
- [Wikipedia 'Variable (high-level programming language)'](https://en.wikipedia.org/wiki/Variable_(high-level_programming_language))
- [Dev.java 'Creating Primitive Type Variables in Your Programs'](https://dev.java/learn/language-basics/primitive-types/)
- [Quora 'Can variables be used in Java without initialization?'](https://www.quora.com/Can-variables-be-used-in-Java-without-initialization)
- [Quora 'Why is String special in Java?'](https://www.quora.com/Why-is-String-special-in-Java)

[^1]: 오버플로우(Overflow), 언더플로우(Underflow)
