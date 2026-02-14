---
title: "[Spring] Spring Core"
description: ""
date: 2026-02-14 09:00:00
update: 2026-02-14 18:00:00
tags:
  - Spring
series:
---

- Spring Core의 핵심은 IoC(Inversion of Control) 컨테이너다.
- Spring은 단순한 라이브러리가 아니라, 객체의 생성과 관계를 대신 관리하는 프레임워크다.

## 1. 개념

### 1.1 IoC(Inversion of Control)

- IoC란 객체의 생성, 의존성 연결, 생명주기 관리의 제어권을 개발자가 아닌 프레임워크가 담당하는 설계 원칙이다.
- 제어권이란 다음 동작을 결정하는 권한을 의미한다.
    - 객체 생성시점
    - 다른 객체와 연결
    - 호출시점

### 1.2 IoC Container

- IoC Container는 다음을 수행한다.
    - BeanDefinition 생성
    - 객체 인스턴스화
    - 의존성 주입
    - 초기화 및 소멸 관리
    - AOP 연계
- 주요 구현체
    - BeanFactory
    - ApplicationContext

### 1.3 DI(Dependency Injection)

- DI는 IoC를 구현하는 대표적인 방식(하위 개념)이다. 객체가 필요로 하는 의존성을 외부에서 주입받는다.
- IoC를 구현하는 방법은 DI 외에도 있다.
    - Service Locator
    - 이벤트 기반 호출
    - 템플릿 메서드 패턴

### 1.4 Bean

- Bean은 IoC Container에 의해 생성, 관리, 조립되는 객체다.
- Spring의 기능(AOP, 트랜잭션, 이벤트 등)을 사용하려면 객체가 반드시 Bean으로 등록해야 한다.

## 2. 왜 필요할까?(문제 상황)

```java
UserRepository userRepository = new UserRepository();
UserService userService = new UserService(userRepository);
```

IoC가 등장하기 전의 코드는 문제점이 있다.

- 강한 결합도
- 테스트 어려움(Mock 주입 불편)
- 객체 생성 책임이 분산됨
- 공통 기능(AOP) 확장이 어려움

특히 규모가 커질수록 객체의 관계는 복잡해지고 객체의 생명주기를 일관되게 관리하기 어렵다. 따라서 IoC는 이러한 문제를 해결하기 위해 등장했다.

## 3. 내부 동작 원리

IoC Container의 흐름은 다음과 같다.

1. BeanDefinition 생성: 정보를 메타 데이터로 저장한다. (클래스 종류, 스코프, 의존성, 초기화 메서드)
2. 객체 생성: Container가 직접 `new`를 수행한다.
3. 의존성 주입: 생성자, setter, 필드 등을 통해 의존성을 연결한다.
4. 초기화 콜백 처리: `@PostConstruct`, InitializingBean, init-method
5. 필요시 프록시(Proxy) 생성: AOP가 적용되는 경우 원본 객체 대신 프록시 객체를 반환한다. 이 시점에 IoC와 AOP가 연결된다.

## 4. 코드 예시

### IoC를 사용하지 않는 상황

```java
public class OrderService {

    private final OrderRepository orderRepository;

    public OrderService() {
        this.orderRepository = new OrderRepository();
    }
}
```

- OrderService와 OrderRepository 구현에 강하게 의존한다.
    - 테스트 코드 작성이 어렵다.

### IoC + DI 적용

```java
public class OrderService {

    private final OrderRepository orderRepository;

    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
}
```

- Spring의 생성 시점에 의존성을 주입한다. 덕분에 이점을 갖는다.
    - 테스트 코드 작성이 편리하다.
    - 확장 가능하다.
    - 결합도가 감소한다.

## 5. 주의점

- DI는 IoC 구현 방식 중 하나일 뿐이다. IoC의 본질은 '제어권 위임'이다.
- 모든 객체를 Bean으로 만들 필요는 없다. 단순 DTO, 도메인 내부 객체는 Bean일 필요가 없다.

## 6. 실무에서의 의미

- IoC가 없다면 다음의 문제가 발생한다.
    - AOP 구현이 어렵다.
    - 트랜잭션 처리가 복잡하다.
    - 테스트 코드 작성 난이도가 증가한다.
    - 확장 포인트가 부족하다.
- IoC 컨테이너 덕분에 이점을 갖는다.
    - 공통 관심사 분리(AOP)
    - 선언적 트랜잭션
    - 의존성 교체 용이
    - 모듈화 용이

즉, Spring의 대부분 기능은 IoC 위에 구축되어 있다.

## 마치며

### Q. IoC는 Spring에서만 유효한 개념일까?

- Spring은 IoC를 널리 알린 대표 사례일 뿐, Spring에 국한된 기술이 아니다. 앞서 '프레임워크가 담당하는 설계 원칙'이라고 말했듯이 다른 프레임워크도 IoC를 사용한다.
- 예를 들어 C# 프레임워크 닷넷(.NET)[^1], JavaScript 프레임워크 NestJS[^2]가 해당한다.

<참고 자료>

- [Spring Framework Documentation 'Core Technologies'](https://docs.spring.io/spring-framework/reference/core.html)
- [『부트캠프 백엔드 개발자 편 with 스프링 부트』(김송아, 한빛미디어, 2026)](https://product.kyobobook.co.kr/detail/S000219025613)

[^1]: [.NET 종속성 주입](https://learn.microsoft.com/ko-kr/dotnet/core/extensions/dependency-injection/overview)
[^2]: [NestJS Custom providers](https://docs.nestjs.com/fundamentals/custom-providers)
