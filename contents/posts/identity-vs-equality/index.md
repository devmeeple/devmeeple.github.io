---
title: "동일성(Identity) vs. 동등성(Equality)"
description: ""
date: 2025-07-13 04:00:00
update: 2025-07-13 18:00:00
tags:
  - Java
series: 
---

객체 지향 언어 Java에서는 어떻게 객체를 비교할까? 객체를 비교하는 핵심 개념, 동일성(Identity)과 동등성(Equality)에 대해 알아보자.

## 동일성과 동등성

### 동일성(Identity)

- 동일성은 두 객체가 같은 메모리 주소를 참조하는지를 의미한다.
- `==` 연산자를 사용하며, 동일한 객체를 참조할 때 `true`를 반환한다.

> `==` 연산자는 값을 비교한다. 기본형(primitive type)에서는 실제값을 비교하고, 참조형(reference type)에서는 참조값을 비교한다.

### 동등성(Equality)

- 동등성은 두 객체의 내용이 같은지를 의미한다.
- `Object`의 `equals()` 메서드를 사용하며, 서로 다른 객체라도 내부 값이 같다면 `true`를 반환한다.

## equals() 메서드 오버라이딩

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

- `Object.equals()`는 오버라이딩 하지 않으면 의도대로 동작하지 않는다. 참조값을 비교한다. 의미 있는 동등성 비교, 실제값을 비교하기 위해서는 오버라이딩이 필요하다.
- `equals()`를 오버라이드 할 때는, 반드시 `hashCode()`도 오버라이드 해야 한다.

## 정리

```java
Coffee americano1 = new Coffee("아메리카노"); // 참조 x001
Coffee americano2 = new Coffee("아메리카노"); // 참조 x002
```

- 동일성과 동등성은 객체 비교에 사용하는 핵심 개념이다.
- 객체에서 `==`는 참조값을 비교하고, `equals()`는 객체의 내용을 비교한다.
- 동일한 객체는 항상 동등하지만, 동등한 객체는 반드시 동일한 객체는 아니다.

**<참고 자료>**

- [김영한 '김영한의 실전 자바 - 중급 1편'](https://inf.run/FiFGQ)

