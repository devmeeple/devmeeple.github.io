---
title: "[Spring] Spring MVC"
description: ""
date: 2026-02-14 15:00:00
update: 2026-02-14 18:00:00
tags:
  - Spring
series:
---

- Spring MVC는 왜 필요하고, 어떻게 동작하며, 실무에서는 어떤 의미를 가질까?

## 1. 개념

### 1.1 MVC

> MVC 다이어그램

- MVC(Model-View-Controller)는 화면과 비즈니스 로직을 분리하기 위한 소프트웨어 설계 패턴이다.
- 관심사를 분리하여 역할, 책임을 강조하고 유지보수성과 확장성을 향상한다.
- 구성 요소
    - Model: 데이터와 비즈니스 로직 관리
    - View: 사용자에게 보이는 화면
    - Controller: Model과 View를 연결
- MVC는 의식적으로 사용하지 않아도 익숙하게 사용할 수 있는 패턴이다.
- Spring Web MVC는 Servlet API[^1] 위에서 동작하는 웹 프레임워크다. 정확히는 Java Servlet API 기반 위에 추상화를 제공한다.
- Spring이 웹 애플리케이션 개발을 단순화하기 위해 등장한 만큼, MVC는 시작부터 핵심 구성 요소였다.
- Spring MVC 외에도 Spring WebFlux(Reactive Stream 기반, 고성능/비동기 스트림에 적합)가 있다.
- 과거 MVC는 서버 중심 구조였다. 하지만 현재는 React, Vue, Fetch API 등이 등장하면서 View와 일부 상태 관리가 클라이언트로 이동했다. 물론 서버에서도 여전히 MVC 구조를 사용한다.

### 1.2 Model

- Model은 애플리케이션의 상태와 비즈니스 로직을 담당한다.
    - 도메인 객체
    - 서비스 로직
    - 데이터 접근 계층
- Model의 변경은 View에도 영향을 준다. 예를 들어 도서 관리 시스템에서 도서를 추가하면 목록 화면도 영향받는다.

### 1.3 View

- View는 사용자에게 보이는 화면이다.
- Spring MVC에서는 보통 템플렛 엔진(Thymeleaf, JSP, Mustache 등)과 JSON 응답(REST API) 형태로 사용한다.

### 1.4 Controller

- Controller는 사용자 요청을 처리하는 진입점이다.
- 요청을 수신, 서비스 호출, Model에 데이터 담기, View 반환 등의 역할을 갖는다.

## 2. 왜 필요할까?(문제 상황)

### MVC가 없던 시절

```kotlin
System.out.println("<html> ...");
```

- Servlet에 모든 코드를 작성하여 HTML과 비즈니스 로직이 섞였다. 이는 유지보수, 테스트가 어려웠다.

### MVC 적용

- 관심사를 분리하여 비즈니스 로직은 Service로, 화면은 View로, 요청 처리는 Controller에 작성한다. 즉, 각 계층이 독립적으로 발전 가능한 구조가 생겼다.

### 3. 내부 동작 원리

> Spring MVC 요청 처리 흐름 다이어그램

1. 클라이언트 요청
2. DispatcherServlet이 요청받음
3. HandlerMapping이 Controller 찾음
4. HandlerAdapter가 실행
5. Model 반환
6. ViewResolver가 View를 결정
7. View 렌더링

## 4. 코드 예시

**Controller**

```java
@Controller
@RequiredArgsController
public class BookController {

    private final BookService bookService;

    @GetMapping("/books")
    public String books(Model model) {
        model.addAttribute("books", bookService.findAll());
        return "books";
    }
}
```

**Service**

```java
@Service
public class BookService {

    public List<Book> findAll() {
        return List.of(new Book("Spring"), "Rod Johnson");
    }
}
```

## 5. 주의점

### 5.1 각 객체의 역할과 책임에 집중하자

- MVC는 단순한 파일 분리가 아닌 역할 분리가 핵심이다.
- **누구의 역할, 책임인가?**
    - Controller: 요청을 받고 흐름을 제어
    - Service: 비즈니스 로직 처리
    - Repository: 데이터 접근
    - View: 화면 표현

### 5.2 관심사의 분리(Separation of Concerns)

**1. Controller에 비즈니스 로직 사용하지 않기**

[잘못된 예시]

```java
@GetMapping("/discount")
public String discount(Model model) {
    int price = 20000;
    
    if (price > 10000) {
        price *= 0.9;
    }
    
    model.addAttribute("price", price);
    return "result";
}
```

- 테스트가 어렵고 재사용이 불가하며 Controller가 비대해진다.

[올바른 예시]

```java
@GetMapping("/discount")
public String discount(Model model) {
    model.addAttribute("price", discountService.applyDiscount(20000));
    return "result";
}
```

**View에 로직을 과도하게 넣지 않기**

- View는 표현을 담당해야 한다.

[View에서 계산을 수행]

```html
<span th:text="${price * 0.9}"></span>
```

- 이렇게 되면 로직이 흩어지고 유지보수가 어렵다. 또한 테스트도 못한다. 계산 같은 비즈니스 로직은 Service가 수행한다.

### 5.3 계층 간 의존성 역전

- 정상적인 의존 방향은 `Controller -> Service -> Repository` 순서다.

```java
@Service
public class OrderService {
    
    private final OrderController orderController;
}
```

- `Service -> Controller`, `Repository -> Service -> Controller`, 하위 계층이 상위 계층을 참조하면 일반적인 구조가 무너지고 순환 참조가 발생할 수 있다. 또한 테스트와 유지보수도 어렵다.
- 따라서 의존성 방향은 항상 위에서 아래로 가야한다. 아래 계층은 위 계층을 모른다. (계층형 아키텍처의 기본 규칙)

## 6. 실무에서의 의미

- Spring MVC는 단순한 패턴이 아니다. 팀 개발의 기본 구조, 테스트 분리, REST API 설계 기반, 대규모 서비스의 구조적 안정성을 제공한다.

## 마치며

- Spring MVC는 화면을 분리하는 단순한 패턴이 아닌 관심사를 분리하여 유지보수성과 확장성을 확보하는 구조적 기반이다.

#### Q. MVC 외에 대안은 없을까?

- MVC 패턴을 확장하여 HMVC, MVP, MVVM 등이 만들어졌다. 하지만 결국 MVC를 기반으로 한다.

<참고 자료>

- [『부트캠프 백엔드 개발자 편 with 스프링 부트』(김송아, 한빛미디어, 2026)](https://product.kyobobook.co.kr/detail/S000219025613)
- [Wikipedia 'Model-view-controller'](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)
- [Spring Framework Documentation 'Spring Web MVC'](https://docs.spring.io/spring-framework/reference/web/webmvc.html)
- [MDN Web Docs 'MVC'](https://developer.mozilla.org/en-US/docs/Glossary/MVC)

[^1]: https://docs.oracle.com/javaee/7/api/javax/servlet/Servlet.html
