---
title: 'Object 클래스'
date: '2026-03-16T18:43:50+09:00'
categories: ["Java"]
tags: ["java.lang", "object class", "toString", "equals"]
draft: true
---

- java.lang 패키지 소개
- Object 클래스
    - Object 다형성
    - Object 배열
- toString()
- Object와 OCP
- equals() - 1. 동일성과 동등성
- equals() - 2. 구현

## java.lang 패키지

```text
- Object
- 래퍼 클래스
- String
- System
- Math
```

- `java.lang`은 Java의 핵심 구성 요소다. Java 프로그래밍 언어의 설계 및 구현에 필수로 사용하는 클래스를 포함한다.
- 모든 프로그램에 자동으로 `import` 구문을 추가한다. 따라서 직접 명시하지 않아도 기능을 사용할 수 있다.

## Object 클래스

- `Object` 클래스는 모든 객체가 반드시 가져야 하는 기본 메서드가 정의되어 있다.
    - `equals(Object obj)`: 현재 객체와 지정된 객체를 비교하여 동일성을 확인한다.
    - `hashCode()`: 객체의 해시 코드 값을 반환한다. 해시 기반 컬렉션에 주로 사용한다.
    - `toString()`

- `extends` 키워드를 사용하여 부모 클래스를 상속하지 않으면 `Object` 클래스를 자동으로 상속한다.
- 다형성의 기본 구현

### Object 다형성

- 모든 클래스의 최상위 부모 클래스는 `Object`다. 따라서 `Object`는 모든 객체를 참조할 수 있다.
- Object 다형성의 한계

### toString()

- `toString()` 메서드는 객체의 정보를 문자열 형태로 제공하여 디버깅과 로깅에 주로 사용한다.
- 오버라이딩 하지 않은 `toString()` 메서드는 클래스 이름과 객체의 해시 코드를 16진수 형식(예: `ClassName@hashCode`)으로 제공한다.
- 오버라이딩 하면 객체의 정보를 다른 형식으로 표현할 수 있다.

## equals()

### 동일성과 동등성

- 동일성(Identity): `==` 연산자를 사용, 두 객체의 참조가 동일한 객체를 가리키는지 확인한다.
- 동등성(Equality): `equals()` 메서드를 사용, 두 객체가 논리적으로 동등한지 확인한다.

> [!NOTE] 동등성은 객체마다 비교하는 기준이 다르다. 따라서 동등성 비교가 필요하면 기본으로 제공하는 `equals` 메서드를 재정의해야 한다. 재정의 하지 않으면 `Object` 클래스는 동일성 비교를 제공한다.

- `equals()` 메서드를 구현하려면 지켜야 하는 까다로운 규칙이 있다. 실무에서는 대부분 IDE의 지원을 받아 `equals()`를 구현한다.
    - 주로 `hashCode()`와 함께 사용한다. 

## 마치며

- 모든 객체의 최상위 부모 클래스는 `Object`다.
- `Object` 클래스가 없는 세상이라면 개발자 마다 공통 기능 클래스를 따로 정의, 사용해야 한다. 제약이 없어 일관성 없는 세상이 펼쳐진다.

### 참고 자료

- [Java Documentation 'java.lang'](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/package-summary.html)
