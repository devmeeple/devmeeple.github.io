---
title: "4. 과일가게 API 구현하기"
description: ""
date: 2024-05-03 20:05:39
update: 2024-05-03 20:05:39
tags:
  - Spring
series: "인프런 워밍업 클럽 - 스터디 BE 1기"
---

3, 4일 차 강의에서는 기본적인 데이터베이스 사용법과 데이터베이스를 사용해 API를 만드는 방법을 배웠다.
학습한 내용을 바탕으로 요구사항을 살펴보자.

> 4일 차 구현과제는 총 3 문제고 각 문제는 이어진다.

## 요구사항

1. 과일가게에 입고되는 과일정보를 추가한다.
2. 팔린 과일의 정보를 저장한다.
3. 과일이름을 기준으로 팔린 금액, 팔리지 않은 금액을 조회한다.

```sql
CREATE TABLE fruit
(
    id               BIGINT AUTO_INCREMENT,
    name             VARCHAR(20) NOT NULL,
    warehousing_date DATE        NOT NULL,
    price            BIGINT      NOT NULL,
    is_sold          TINYINT(1) NOT NULL DEFAULT 0
    PRIMARY KEY (id)
);
```

```java

@RequestMapping("/api/v1/fruit")
@RestController
public class FruitController {
}
```

강의에서 다룬 내용을 바탕으로 테이블과 컨트롤러를 선언했다.

> Q. 만약 테이블을 이미 선언했다면 했다면 어떻게 할까?

`ALTER TABLE [테이블명] ADD [컬럼명] [타입] [옵션];`과 같은 형식으로 컬럼을 추가한다.

## 문제 1) 과일정보 추가하기

| 메서드  | URL           |
|------|---------------|
| POST | /api/v1/fruit |

### 요청

| 이름              | 타입        | 설명   | 필수 |
|-----------------|-----------|------|----|
| name            | String    | 과일명  | O  |
| warehousingDate | LocalDate | 입고날짜 | O  |
| price           | long      | 가격   | O  |

### 예제

**요청**

```shell
http POST :8080/api/v1/fruit name=사과 warehousingDate=2024-02-01 price=5000
```

```json
{
  "name": "사과",
  "warehousingDate": "2024-02-01",
  "price": 5000
}
```

**응답: 성공**

### 해결

1번 문제의 경우 요청형식은 정의되어 있지만 응답은 상태코드를 반환한다. 문제 해결을 위해서 요청 객체(DTO)가 필요하다.

```java
public class AddFruitIRequest {
    private final String name;
    private final LocalDate warehousingDate;
    private final long price;

    public AddFruitIRequest(String name, LocalDate warehousingDate, long price) {
        this.name = name;
        this.warehousingDate = warehousingDate;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public LocalDate getWarehousingDate() {
        return warehousingDate;
    }

    public long getPrice() {
        return price;
    }
}
```

```java

@PostMapping
public void addFruit(@RequestBody AddFruitIRequest request) {
    String sql = "INSERT INTO fruit (name, warehousing_date, price) VALUES (?, ?, ?)";
    jdbcTemplate.update(sql, request.getName(), request.getWarehousingDate(), request.getPrice());
}
```

데이터베이스에 데이터를 추가하기 위해서는 DML(Data Manipulation Language) 중 하나인 INSERT 문을 사용한다. 응답형식은 따로 정해져 있지 않아 반환하지 않았다.

> Q. 정수를 다루는 대표적인 방법은 int와 long이 있다. 왜 long을 사용했을까?

애플리케이션의 확장을 고려하여 long형식으로 선언했다고 생각한다. 데이터베이스에서 BIGINT 형식으로 테이블을 선언한 것과 같은 이유다.

## 문제 2) 과일정보 수정

| 메서드 | URL           |
|-----|---------------|
| PUT | /api/v1/fruit |

### 예제

**요청**

```shell
http PUT :8080/api/v1/fruit id=3
```

```json
{
  "id": 3
}
```

**응답: 성공**

### 해결

```java

@PutMapping
public void updateFruit(@RequestBody UpdateFruitRequest request) {
    String readSql = "SELECT * FROM fruit WHERE id = ?";
    boolean isFruitNotExist = jdbcTemplate.query(readSql, (rs, rowNum) -> 0, request.getId()).isEmpty();

    if (isFruitNotExist) {
        throw new IllegalArgumentException("과일을 찾을 수 없습니다");
    }

    String sql = "UPDATE fruit SET is_sold = 1 WHERE id = ?";
    jdbcTemplate.update(sql, request.getId());
}
```

가장 애를 먹었다. 컨트롤러는 강의에서 다룬 형식과 같다. 하지만 요청객체 선언은 수정이 필요했다. 기존과 같은 방법으로 선언했을 때는 문제가 해결되지 않았다. 반복적으로 400 Bad Request가 발생했다.

> 400 상태코드는 클라이언트에서 잘못된 형식으로 요청할 때 발생한다.

> JSON parse error: Cannot construct instance of

Spring은 직렬화/역직렬화에 Jackson 라이브러리를 사용한다. Jackson은 기본생성자가 없으면 동작하지 않는다.
총 3가지 방법으로 문제를 해결할 수 있었다.

1. 기본 생성자를 생성한다: 기본 생성자를 생정하면 `final` 를 사용할 수 없다.
2. 임의의 필드를 추가한다: 현재는 `id` 필드만 있지만 다른 필드를 추가하면 동작한다.
3. 방식을 지정한다.

3번으로 문제를 해결하기 위해서는 Jackson의 동작방식을 알아봤다. Jackson은 두 가지의 방식으로 데이터를 변환한다.

- Properties: 기본적인 변환방식
- Delegating: 복잡한 데이터가 있거나 데이터 처리방법을 변경할 때 사용

> 필드가 1개인 상태에서 Properties 방식으로 변환하려면 어떻게 해야 할까?

```java

public class UpdateFruitRequest {
    private final long id;

    @JsonCreator
    public UpdateFruitRequest(@JsonProperty("id") long id) {
        this.id = id;
    }

    public long getId() {
        return id;
    }
}
```

`@JsonCreator`, `@JsonProperty` 어노테이션을 사용한다. 두 어노테이션을 사용하면 기본생성자와 setter 없이도 객체를 생성하여 불변객체를 선언할 수 있다.

2번 문제도 앞선 1번 문제처럼 응답형식이 정해져 있지 않다. 아무것도 반환하지 않는다.

## 문제 3) 과일이름을 기준으로 팔린금액, 팔리지 않는 금액 조회

```text
1. (1, 사과, 3000원, 판매 O)
2. (2, 사과, 4000원, 판매 X)
3. (3, 사과, 3000원, 판매 O)
```

| 메서드 | URL                |
|-----|--------------------|
| GET | /api/v1/fruit/stat |

### 요청

**쿼리 파라미터**

| 이름   | 타입     | 설명  | 필수 |
|------|--------|-----|----|
| name | String | 과일명 | O  |

### 예제

**요청**

```shell
http :8080/api/v1/fruit\?name=사과
```

**응답: 성공**

```json
{
  "salesAmount": 6000,
  "notSalesAmount": 4000
}
```

### 해결

3번 문제는 이전 문제들과 다르게 응답형식이 지정되어 있다. 따라서 응답 객체를 선언해야 한다.

```java
public class FruitSalesResponse {
    private final long salesAmount;
    private final long notSalesAmount;

    public FruitSalesResponse(long salesAmount, long notSalesAmount) {
        this.salesAmount = salesAmount;
        this.notSalesAmount = notSalesAmount;
    }

    public long getSalesAmount() {
        return salesAmount;
    }

    public long getNotSalesAmount() {
        return notSalesAmount;
    }
}
```

```java

@GetMapping("/stat")
public FruitSalesResponse findByName(@RequestParam String name) {
    String sql = "SELECT SUM(price) FROM fruit WHERE name = ? GROUP BY is_sold";
    List<Long> salesAmounts = jdbcTemplate.query(sql, (rs, rowNum) -> rs.getLong(1), name);

    Long salesAmount = salesAmounts.get(0);
    Long notSaleAmount = salesAmounts.get(1);

    return new FruitSalesResponse(salesAmount, notSaleAmount);
}
```

처음부터 SUM, GROUP BY를 사용했다. 이외에는 이전과제와 강의에서 다루는 내용과 일치한다.

## 마무리

강의가 진행됨에 따라 컨트롤러의 역할이 증가하고 있다. 역할을 분리하는 리팩터링이 필요한 시간이다. 다음 강의와 과제가 기대된다.

### 함께 자라기

- [MySQL BOOLEAN by 당큰 테크 블로그](https://medium.com/daangn/mysql-boolean-%EC%BB%AC%EB%9F%BC-7abd9b35c664)
- [SQL 가독성을 높이는 다섯 가지 사소한 습관](https://yozm.wishket.com/magazine/detail/1519/)
- [Jackson by GitHub](https://github.com/FasterXML/jackson)
