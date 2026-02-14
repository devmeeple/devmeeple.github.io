---
title: "[Spring] Controller와 HTTP 이해하기"
description: ""
date: 2026-02-14 23:00:00
update: 2026-02-14 23:30:00
tags:
  - Spring
series:
---

## 1. 개념

### 1.1 HTTP

- HTTP(HypeText Transfer Protocol)은 클라이언트와 서버가 데이터를 주고받기 위한 통신 규약이다.
- 요청(Request)과 응답(Response) 구조를 사용한다.

### 1.2 웹 서버 vs. WAS

**1.2.1 웹 서버**

- 웹 서버(Web Server)는 정적 리소스(HTML, CSS, JS, 이미지)를 처리한다.
- 대표적으로 Apache, Nginx가 해당한다.

**1.2.2 WAS**

- WAS(Web Application Server)는 동적인 요청을 처리한다.
- Servlet 컨테이너를 포함한다.
- 대표적으로 Tomcat, Jetty가 해당한다.
- Spring Boot는 기본적으로 Tomcat(WAS)를 내장하고 있다.

### 1.3 Controller

```java

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    @GetMapping("/{id}")
    public UserResponse getUser(@PathVariable Long id) {
        return userService.findById(id);
    }
}
```

- Controller는 HTTP 요청을 받아 적절한 비즈니스 로직으로 연결하는 진입점이다.

## 2. 왜 필요할까?(문제 상황)

### 2.1 Controller가 없는 세상

```text
HTTP 요청 -> 파싱 -> URL 분석 -> 로직 실행 -> JSON 변환 -> 응답 생성
```

- HTTP 요청을 직접 파싱해야 한다.
- URL을 직접 분기 처리해야 한다.
- JSON 변환을 직접 처리해야 한다.
- 예외 처리도 직접 해야 한다.

### 2.2 Controller가 구원하는 세상

- Spring은 URL 매핑, HTTP Method 매핑, JSON과 객체 변환, 상태 코드 처리, 예외 처리를 전부 처리해 준다.
- 개발자가 '비즈니스 로직'에 집중할 수 있는 환경을 제공한다.

## 3. 내부 동작 원리

1. 클라이언트
2. 웹 서버(Apache/Nginx)
3. WAS(Tomcat)
4. DispatcherServlet
5. HandlerMapping
6. Controller
7. Service
8. Response 반환

**Spring 내부 흐름**

1. HTTP 요청을 수신한다.
2. DispatcherServlet이 모든 요청을 받는다.
3. HandlerMapping이 적절한 Controller를 탐색한다.
4. HandlerAdapter가 메서드를 실행한다.
5. HttpMessageConverter가 JSON을 변환한다.
6. HTTP Response를 반환한다.

## 4. 코드 예시

### 4.1 GET 요청

```java
@GetMapping("/users/{id}")
public ResponseEntity<UserResponse> findUser(@PathVariable Long id) {
    return ResponseEntity.ok(userService.findById(id));
}
```

### 4.2 POST 요청

```java
@PostMapping("/users")
public ResponseEntity<Void> create(@RequestBody CreateUserRequest request) {
    userService.create(request);
    return ResponseEntity.status(HttpStatus.CREATED).build();
}
```

### 4.3 PUT과 PATCH 요청

**PUT(전체 수정)**

```java
@PutMapping("/users/{id}")
public void update(@PathVariable Long id, @RequestBody UpdateUserRequest request) {
    userService.updateAll(id, request);
}
```

```PATCH(부분 수정)```

```java
@PatchMapping("/users/{id}")
public void partialUpdate(@PathVariable Long id, @RequestBody UpdateUserRequest request) {
    userService.partialUpdate(id, request);
}
```

## 5. 주의점

- 복잡한 비즈니스 로직을 Controller에 넣지 않는다. Service에 책임을 넘긴다.
- HTTP Method 의미를 맞게 사용한다.
  - GET: 조회
  - POST: 생성
  - PUT: 전체 수정
  - PATCH: 부분 수정
  - DELETE: 삭제

## 6. 실무에서의 의미

### 6.1 RESTfUl 설계의 핵심

- Controller는 단순한 요청을 받는 계층이 아닌 'API 설계의 얼굴'이다. URL 구조와 HTTP Method는 시스템 설계 철학을 드러낸다.

## 마치며

- 좋은 Controller를 설계해야 좋은 API 설계도 이어진다.

### Q. 실무에서 데이터를 수정할 때 PUT을 정말 더 많이 사용할까?

- PATCH가 까다롭다고 언급하는 이유는 다음과 같다.
    - `null` 처리
    - 어떤 필드가 변경되었는지 구분 필요
    - 복잡한 DTO 설계
    - JsonMergePatch 등 추가 처리 필요

하지만 명확한 부분 수정 요구와 명확한 REST 설계에 PATCH 사용은 적절한 방법이다.
