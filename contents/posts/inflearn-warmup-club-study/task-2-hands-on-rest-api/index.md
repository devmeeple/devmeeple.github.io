---
title: "2. API 실습"
description: ""
date: 2024-04-30 18:06:35
update: 2024-04-30 18:06:35
tags:
  - Spring
series: "인프런 워밍업 클럽 - 스터디 BE 1기"
---

![인프런 워밍업 클럽 - 스터디 1기](../images/inflearn-warmup-club-study.png)

2일 차는 첫 HTTP API 개발을 주제로 간단한 API를 만들었다. 배운 건 써봐야지. 먼저 과제의 요구사항을 검토하고 구현해 보자.

> 모든 코드는 [GitHub](https://github.com/devmeeple/inflearn-warmup-club-study/tree/feature/week-1)에서 확인할 수 있습니다.

## 문제 1

두 수를 입력하면 덧셈, 뺄셈, 곱셈결과를 반환한다.

**기본 정보**

| 메서드 | URL          |
|-----|--------------|
| GET | /api/v1/calc |

### 요청

**쿼리 파라미터**

| 이름   | 타입  | 설명      | 필수 |
|------|-----|---------|----|
| num1 | int | 첫 번째 숫자 | O  |
| num2 | int | 두 번째 숫자 | O  |    |

### 예제

**요청**

```shell
http :8080/api/v1/calc\?num1\=10\&num2\=5
```

**응답: 성공**

```json
{
  "add": 15,
  "minus": 5,
  "multiply": 50
}
```

### 해결

문제를 살펴보면 요청은 `/api/v1/{필요 API}`와 같고, 응답은 `JSON`형식임을 알 수 있다.

```java

@RestController
@RequestMapping("/api/v1")
public class TaskController {
}
```

따라서 위와 같이 선언할 수 있다. 이어서 응답과 요청에 맞는 객체를 선언한다.

- TaskCalcRequest
- TaskCalcResponse

```java

@GetMapping("/calc")
public TaskCalcResponse calcTwoNumbers(TaskCalcRequest request) {
    return new TaskCalcResponse(
            request.getNum1() + request.getNum2(),
            request.getNum1() - request.getNum2(),
            request.getNum1() * request.getNum2()
    );
}
```

객체를 선언하고 최종완성된 코드는 위와 같다.

> 응답객체의 덧셈, 뺄셈, 곱셈 계산을 다른 객체에 위임했다면 가독성이 더 좋을 것 같다. 하지만 아직 웹 계층만을 다루고 차후 리팩터링 예정으로 확인되어 레이어를 분리하지 않았다.
>
> 레이어 개념을 학습하면 리팩터링 필요한 코드다.

작성된 코드의 결과를 확인해 보자.

![[문제 1] 덧셈, 뺄셈, 곱셈결과 반환](images/calc.png)

## 문제 2

날짜를 입력하면, 어떤 요일인지 반환한다.

**기본 정보**

| 메서드 | URL                 |
|-----|---------------------|
| GET | /api/v1/day-of-week |

### 요청

**쿼리 파라미터**

| 이름          | 타입     | 설명                         | 필수 |
|-------------|--------|----------------------------|----|
| day-of-week | String | ISO 8601(YYYY-MM-DD)으로 변환됨 | O  |

### 예제

**요청**

```shell
http :8080/api/v1/day-of-the-week\?date\=2023-01-01
```

**응답: 성공**

```json
{
  "dayOfTheWeek": "SUN"
}
```

### 해결

문제를 해결하는 과정은 문제 1과 유사하다. 하지만 이번엔 응답객체만 선언했다.

- TaskDayOfTheWeekResponse

```java

@GetMapping("/day-of-the-week")
public TaskDayOfTheWeekResponse findDayOfTheWeek(@RequestParam @DateTimeFormat(iso = DateTimeFormat.ISO.DATE) LocalDate date) {
    return new TaskDayOfTheWeekResponse(date.getDayOfWeek().getDisplayName(TextStyle.SHORT, Locale.US).toUpperCase());
}
```

문제해결의 열쇠는 `LocalDate` 객체 다루 기다. Java SE8에 도입된 LocalDate는 정말 많이 사용하는 객체다. 사용법이 익숙하지 않다면 꼭 짚고 넘어가야 한다.

> LocalDate 타입으로 변환되기 위해서
>
> @DateTimeFormat(iso = DateTimeFormat.ISO.DATE)를 선언해야 한다.

![[문제 2] 어떤 요일인지 반환](images/day-of-the-week.png)

## 문제 3

여러 수를 입력받아 총합을 반환한다.

**기본 정보**

| 메서드  | URL         |
|------|-------------|
| POST | /api/v1/sum |

### 요청

**본문**

| 이름      | 타입            | 설명    | 필수 |
|---------|---------------|-------|----|
| numbers | List<Integer> | 숫자 배열 | O  |

### 예제

**요청**

```shell
http POST :8080/api/v1/sum
```

**응답: 성공**

```text
15
```

### 해결

![[문제 3] 수의 총합 반환](images/sum.png)

```java

@PostMapping("/sum")
public Integer sumNumbers(@RequestBody TaskSumNumbersRequest request) {
    return request.getNumbers().stream().mapToInt(Integer::valueOf).sum();
}
```

람다를 사용하여 값을 반환했다. 람다 외에도 `for`문과 같은 일반적인 루프도 문제를 해결할 수도 있다. 하지만 다음과제가 람다식인것을 참고하여 미리 적용했다. 자세한 내용은 다음과제에 살펴보자.

## 마치며

요구사항 외에도 람다와 테스트코드를 학습했다. 아직 레이어가 분리되지 않아서 그런지 간단하게 작성됐다. 코드를 리팩터링 하고 레이어가 분리되면 어떤 식으로 작성해야 할지 추가학습이 필요하다.

코드를 미리 준비했음에도 불구하고 정리하는데 꽤 오랜 시간이 소요됐다. 일상으로 돌아가 글을 어떤 순서로 작성하면 좋을지 한번 더 생각해 보자.

### 함께 자라기

- [Java의 날짜와 시간 API](https://d2.naver.com/helloworld/645609)
- [Testing the Web Layer](https://spring.io/guides/gs/testing-web)

