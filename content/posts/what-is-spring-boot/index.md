---
title: '스프링 부트, 누구냐 넌 - 핵심 개념과 내부 동작 정리'
date: '2026-04-05T21:18:56+09:00'
categories: ["Spring"]
tags: ["spring-boot", "IoC", "di", "aop", "bean", "java"]
---

![스프링 부트 누구냐 넌<출처: 올드보이>](oldboy.jpg '스프링 부트 누구냐 넌 <출처: 올드보이>')

스프링(Spring)은 국내 채용 공고에서 압도적인 존재감을 뽐낸다. 스프링 부트(Spring Boot)와 차이점은 무엇일까? 어쩌다 등장했을까?

이 글을 통해 스프링 부트의 등장 배경부터 내장 웹 서버, 자동 구성, IoC/DI, 빈(Bean), AOP까지 스프링 부트를 이해하는데 필요한
핵심 개념을 알아보자.

## 1. 왜 스프링 부트일까?

스프링 프레임워크는 어느덧 자바 엔터프라이즈 개발의 사실상 표준으로 자리 잡았다. 하지만 초기 스프링은 진입 장벽이 높았다. 
애플리케이션을 하나 만들려면 수십 줄의 XML 설정 파일이 필요했고 라이브러리 간 버전 충돌 문제가 빈번했다. 
Tomcat 같은 웹 서버도 별도로 설치하고 배포 파일을 따로 만들어야 했다.

[스프링 부트는 이런 불편함을 해결하기 위해 2014년 4월 1일 처음 등장했다.](https://spring.io/blog/2014/04/01/spring-boot-1-0-ga-released) 핵심 목표는 다음과 같다.

> "설정보다 관례(CoC, Convention over Configuration)" - 개발자가 비즈니스 로직에 집중할 수 있도록 반복적인 설정은 스프링 부트가 대신 처리한다.

오늘날 스프링 부트는 REST API 서버, 마이크로서비스 아키텍처, 배치 처리, 관리자 도구 등 자바 백엔드 개발의 사실상 모든 영역에서 사용한다.

## 2. 스프링 부트의 내부 구조 - 4가지 핵심 기능

스프링 부트가 '편리하다'라고 느껴지는 이유는 크게 4가지 핵심 기능 덕분이다.

### 2.1 내장 웹버 서버(Embedded Server)

기존 스프링 애플리케이션을 배포하려면 Tomcat을 별도로 설치, `WAR` 파일을 만들어 서버에 올리는 과정이 필요했다. 
반면 스프링 부트는 Tomcat을 애플리케이션 안에 내장, `JAR` 파일 하나만 실행하면 서버가 바로 시작된다.

```shell
java -jar my-application.jar
```

내장 웹 서버 덕분에 개발과 배포가 훨씬 간편해졌다.

### 2.2 스타터(Starter)

```groovy
dependencies {
    implementation "org.springframework.boot:spring-boot-starter-web"
}
```

웹 개발은 Spring MVC, Jackson, Tomcat 등 여러 라이브러리를 함께 사용한다. 과거에는 각각의 라이브러리와 호환되는 버전을 개발자가 직접 찾아 등록해야 했다.

스타터는 관련 의존성을 하나의 묶음으로 제공한다. 예를 들어 `spring-boot-starter-web` 하나만 추가하면 웹 개발에 필요한 라이브러리가 버전 충돌 없이 한꺼번에 추가된다.

### 2.3 자동 구성(Auto Configuration)

사실 스타터로 의존성을 추가하면 끝이 아니다. 관련 설정이 필요하다. 하지만 스프링 부트는 관련 설정도 자동으로 처리해 준다. 이것이 자동 구성이다.

예를 들어 `spring-boot-starter-data-jpa`를 추가할 때 스프링 부트는 JPA 관련 설정을 자동으로 처리한다. 
덕분에 개발자는 `application.yml`[^1]에 데이터베이스 접속 정보만 입력하면 된다.

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password
```

> 내부적으로는 [@EnableAutoConfiguration](https://docs.spring.io/spring-boot/reference/using/auto-configuration.html) 어노테이션과 `META-INF/spring.factories` 파일을 통해 조건에 맞는 설정 클래스들이 자동으로 로드되는 방식으로
> 동작한다.

### 2.4 액츄에이터(Actuator)

| 엔드포인트               | 설명              |
|---------------------|-----------------|
| `/actuator/health`  | 애플리케이션 상태 확인    |
| `/actuator/metrics` | CPU, 메모리 등 성능 지표 |
| `/actuator/env`      | 환경변수 및 설정 값 확인  |

[운영 중인 애플리케이션의 상태를 모니터링 하고 관리할 수 있는 기능을 제공한다.](https://docs.spring.io/spring-boot/reference/actuator/index.html) `spring-boot-starter-actuator`를 추가하면 엔드포인트가 자동으로 생성된다.
덕분에 별도의 모니터링 코드를 작성하지 않아도 운영에 필요한 정보를 바로 확인할 수 있다.

## 3. 스프링의 핵심 철학 - IoC와 DI

스프링 부트의 편리함 뒤에는 스프링 프레임워크의 핵심 철학, IoC(제어의 역전)와 DI(의존성 주입)가 있다.

### 3.1 제어의 역전(IoC, Inversion of Control)

```java
// 개발자가 직접 객체를 생성
OrderService orderService = new OrderService();
```

일반적인 프로그래밍에서는 개발자가 직접 객체를 생성하고 관리한다. IoC는 제어권을 프레임워크에게 넘긴다. 객체를 언제, 어떻게 만들지 스프링이 결정한다.
개발자는 필요한 객체를 선언만 하면 된다.

식당에 비유하면, 손님(개발자)은 직접 요리(객체 생성)를 하지 않고, 주문(선언)만 하면 주방장(스프링)이 알아서 요리를 내어주는 것이다.

### 3.2 의존성 주입(DI, Dependency Injection)

```java
// DI 없이 - 직접 생성
public class OrderService {
    private PaymentService paymentService = new PaymentService(); // 강한 결합
}

// DI 적용 - 외부에서 주입
@Service
public class OrderService {
    private final PaymentService paymentService;
    
    @Autowired // 스프링이 PaymentService를 자동으로 주입
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

DI를 사용하면 `OrderService`는 `PaymentService`가 어떻게 만들어지는지 알 필요가 없다. 테스트 할 때도 가짜 객체(Mock)[^2]로 쉽게 교체할 수 있어 유지보수성이
크게 높아진다.

## 4. 빈(Bean)과 IoC 컨테이너

**빈(Bean)이란?**

```java
@Service // 스프링이 관리하는 빈으로 선언
public class UserService {
    // ...
}
```

스프링에서 빈(Bean)은 IoC 컨테이너가 생성하고 관리하는 객체를 의미한다. 모든 자바 객체가 빈이 되는 것은 아니다. 
빈이 되려면 `@Component`, `@Service`, `@Repository`, `@Controller` 같은 어노테이션을 붙이거나, `@Bean`으로 명시적으로 등록해야 한다.

**IoC 컨테이너란?**

IoC 컨테이너는 빈의 생성, 의존성 연결, 생명주기 관리를 담당하는 스프링의 핵심 엔진이다. `ApplicationContext`가 대표적인 IoC 컨테이너 구현체다.
애플리케이션을 시작하면 IoC 컨테이너는 다음 순서로 동작한다.

1. 빈으로 등록된 클래스 스캔
2. 의존 관계를 파악, 순서에 맞게 객체 생성
3. 의존성을 주입하여 연결
4. 애플리케이션 종료 시 빈을 소멸

개발자는 이러한 과정을 직접 관리할 필요 없이, 필요한 빈을 선언하고 가져다 쓰기만 하면 된다.

## 5. AOP - 관점 지향 프로그래밍

**반복되는 부가 로직 문제**

```java
public void createOrder(Order order) {
    log.info("createOrder 시작"); // 부가 로직 (1)
    transaction.begin(); // 부가 로직 (2)
    
    // 실제 핵심 비즈니스 로직
    orderRepository.save(order);
    
    transaction.commit(); // 부가 로직 (3)
    log.info("createOrder 종료"); // 부가 로직 (4)
}
```

실제 서비스를 개발하다 보면 핵심 비즈니스 로직과 관련 없는 코드가 여럿 반복되는 상황이 발생한다. 대표적으로 로깅과 트랜잭션 처리가 있다.
이런 코드가 수십, 수백 개의 메서드에 흩어지면 유지보수가 매우 어려워진다.

**AOP의 해결 방식**

AOP(Aspect-Oriented Programming, 관점 지향 프로그래밍)는 이런 부가 로직을 핵심 로직에서 분리하여 한 곳에서 관리할 수 있게 지원한다.

```java
@Aspect
@Component
public class LoggingAspect {
    
    @Around("execution(* com.example.service.*.*(..))") // 서비스 패키지의 모든 메서드에 적용
    public Object log(ProceedingJoinPoint joinPoint) throws Throwable {
        log.info("{} 시작", joinPoint.getSignature().getName());
        Object result = joinPoint.proceed(); // 핵심 로직 실행
        log.info("{} 종료", joinPoint.getSignature().getName());
        return result;
    }
}
```

`service` 패키지 안의 모든 메서드에 로깅을 자동으로 적용, 핵심 로직은 부가 로직을 전혀 알 필요가 없다. 
스프링에서 트랜잭션 처리에 쓰이는 [`@Transactional`](https://docs.spring.io/spring-framework/reference/data-access/transaction/declarative/annotations.html)도 AOP를 기반으로 동작한다.

## 마치며

사실 지금까지 살펴본 개념은 하나의 흐름으로 연결된다.  

스프링 부트는 스타터로 필요한 라이브러리를 묶어 제공하고, 자동 구성으로 설정을 대신 처리한다. 내장 웹 서버 덕분에 별도의 서버 설치 없이 바로 실행할 수 있고, 액츄에이터로 운영 상태를 모니터링링할 수 있다.

모든 것의 기반은 IoC 컨테이너다. 컨테이너는 빈을 생성하고 DI로 연결하며, AOP를 통해 부가 로직을 핵심 로직으로부터 깔끔하게 분리한다.

처음에는 개념이 많아 복잡하게 느껴지지만 결국 스프링 부트의 모든 기능은 '개발자가 비즈니스 로직에 집중할 수 있는 환경을 제공한다' 하나의 목표를 향한다.

[^1]: `application.properties`와 동일하다.
[^2]: 단위 테스트 시 실제 객체 대신 사용하는 가짜 객체, 외부 의존성을 제거하고 특정 동작을 흉내 내어 테스트 대상 코드의 로직만 검증하는 데 사용한다. 
Mockito 같은 프레임워크로 주로 생성하여 메서드 호출 여부를 검증하거나 사전에 정의된 결과를 반환하는 데 사용한다.

