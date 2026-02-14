---
title: "[Spring] Model(Service, Repository, DI)"
description: ""
date: 2026-02-14 23:30:00
update: 2026-02-14 23:50:00
tags:
  - Spring
series:
---

## 1. 개념

- Spring에서 Model은 단순한 '데이터 객체'를 의미하지 않는다.
- 애플리케이션의 비즈니스 규칙을 담당하는 계층을 의미한다.

```text
Controller -> Service -> Repository -> Database
```

- 일반적으로 위와 같이 나뉜다.

### 1.1 Service

- 비즈니스 로직 담당
- 트랜잭션 처리
- 여러 Repository 조합

### 1.2 Repository

- 데이터 접근 계층(Persistence Layer)
- Database와 직접 통신

## 2. 왜 필요할까?(문제 상황)

### 2.1 Controller에 모든 로직을 사용하는 세상

```java
@PostMapping("/order")
public String order() {
    // 데이터베이스 접근
    // 가격 계산
    // 재고 감소
    // 결제 처리
}
```

- Controller에 모든 로직이 들어가면 다음과 같은 문제가 발생한다.
    - 테스트가 어렵다.
    - 코드 재사용이 어렵다.
    - 유지보수 비용이 증가한다.
    - 책임이 섞여 SRP를 위반한다.

### 2.2 역할을 분리하는 세상

```java
@PostMaiing("/order")
public String order() {
    orderService.order();
}
```

- 관심사의 분리(Separation of Concerns)
    - Controller는 HTTP 요청을 처리한다.
    - Service는 비즈니스 로직만 담당한다.
    - Repository는 Database 접근을 담당한다.

## 3. 내부 동작 원리

- Spring은 Model 계층을 Bean으로 관리한다.
- `@Service`, `@Repository` 어노테이션을 사용하면 다음과 같은 과정이 이뤄진다.
  1. Component Scan
  2. Bean 등록
  3. DI 수행
  4. 필요시 Proxy 생성(AOP, 트랜잭션)
- 즉, 개발자가 `new` 하지 않아도 컨테이너가 객체를 생성하고 주입한다.

## 4. 코드 예시

### 4.1 Service

```java
@Service
public class OrderService {
    
    private final OrderRepository orderRepository;
    
    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
    
    public void order() {
        orderRepository.save(new Order());
    }
}
```

### 4.2 Repository

```java
@Repository
public class OrderRepository {
    
    public void save(Order order) {
        // Database 저장 로직
    }
}
```

## 5. DI 주입 방식 정리

### 5.1 필드 주입

```java
@Autowired
private OrderRepository orderRepository;
```

- 장점: 코드가 간결하다.
- 단점
  - 테스트가 어렵다.
  - `final` 사용이 불가능하다.
  - 순환참조가 발생할 때 감지가 어렵다.

### 5.2 Setter 주입

```java
@Autowired
public void setOrderRepository(OrderRepository orderRepository) {
    this.orderRepository = orderRepository;
}
```

- 장점: 선택적 의존이 가능하다.
- 단점: 객체의 불변성을 보장하지 않는다.

### 5.3 생성자 주입(권장)

```java
public OrderService(OrderRepository orderRepository) {
    this.orderRepository = orderRepository;
}
```
- 생성자 주입은 Spring에서 공식으로 권장하는 방식이다.

- 장점
  - 객체의 불변성을 보장한다.
  - 테스트가 쉽다.
  - 순환참조가 발생할 때 컴파일 시점에 확인할 수 있다.
  - `final`을 사용할 수 있다.

## 6. 실무에서의 의미

- 실무에서 Model 계층은 단순 CRUD 계층이 아니다.

```java
@Transactional
public void order() {
}
```

- Service는 트랜잭션 경계다.
- Repository는 데이터 접근만 담당해야 한다. 

## 7. 마치며

- Spring에서 Model은 단순한 계층 분리가 아니다. 애플리케이션의 복잡도를 통제하기 위한 전략이다.

### Q. 비즈니스 로직, 도메인 로직이란?

**비즈니스 로직**

- 비즈니스 로직이란 서비스가 제공하는 기능의 규칙(재고가 0이면 주문을 할 수 없다)을 의미한다.

**도메인 로직**

- 도메인 객체가 스스로 가지는 규칙을 의미한다.
- 도메인 객체 안에 규칙이 존재하면 객체지향적 설계에 가까워진다.
