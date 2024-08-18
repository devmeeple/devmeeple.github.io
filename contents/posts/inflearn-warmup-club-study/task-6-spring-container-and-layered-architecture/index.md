---
title: "6. 스프링 컨테이너와 계층화 아키텍처(Layered Architecture)"
description: ""
date: 2024-05-13 16:49:08
update: 2024-05-13 16:49:08
tags:
  - Spring
series: "인프런 워밍업 클럽 - 스터디 BE 1기"
---

![인프런 워밍업 클럽 - 스터디 1기](../images/inflearn-warmup-club-study.png)

6일 차는 **스프링 컨테이너의 의미와 사용 방법**을 주제로 스프링 컨테이너가 왜 필요한지, 어떻게 기존의 코드를 리팩터링 할 수 있는지 배웠다. 주어진 과제는 총 2문제로 계층화 아키텍처(Layered
Architecture) 리팩터링 하기, 스프링 빈(Spring Bean)을 다룰 수 있는지 확인한다.

## 요구사항

- 문제 1: [과제 4](https://devmeeple.github.io/task-4-fruit-store-api/)에서 만들었던 API를 Controller -Service - Repository로 분리하기
- 문제 2:
    1. 분리된 저장소(FruitRepository)를 FruitMemoryRepository, FruitMySqlRepository로 나누기
    2. `@Primary` 어노테이션을 활용해 Repository를 바꿔가며 동작할 수 있도록 변경하기

## 문제 1

```java

@RequestMapping("/api/v1/fruit")
@RestController
public class FruitController {

    private final JdbcTemplate jdbcTemplate;

    public FruitController(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    @PostMapping
    public void addFruit(@RequestBody AddFruitIRequest request) {
        String sql = "INSERT INTO fruit (name, warehousing_date, price) VALUES (?, ?, ?)";
        jdbcTemplate.update(sql, request.getName(), request.getWarehousingDate(), request.getPrice());
    }

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

    @GetMapping("/stat")
    public FruitSalesResponse findByName(@RequestParam String name) {
        String sql = "SELECT SUM(price) FROM fruit WHERE name = ? GROUP BY is_sold";
        List<Long> salesAmounts = jdbcTemplate.query(sql, (rs, rowNum) -> rs.getLong(1), name);

        Long salesAmount = salesAmounts.get(0);
        Long notSaleAmount = salesAmounts.get(1);

        return new FruitSalesResponse(salesAmount, notSaleAmount);
    }
}
```

이전에 작성된 코드는 Controller가 HTTP와 관련된 기능 외에 다양한 기능을 포함하고 있다. 요구사항에 맞게 분리해 보자.

### Controller

```java

@RequestMapping("/api/v1/fruit")
@RestController
public class FruitController {

    private final FruitService fruitService;

    public FruitController(FruitService fruitService) {
        this.fruitService = fruitService;
    }

    @PostMapping
    public void addFruit(@RequestBody AddFruitRequest request) {
        fruitService.addFruit(request);
    }

    @PutMapping
    public void updateFruit(@RequestBody UpdateFruitRequest request) {
        fruitService.updateFruit(request);
    }

    @GetMapping("/stat")
    public FruitSalesResponse findByName(@RequestParam String name) {
        return fruitService.findByName(name);
    }
}
```

### Service

```java

@Service
public class FruitService {

    private final FruitRepository fruitRepository;

    public FruitService(FruitRepository fruitRepository) {
        this.fruitRepository = fruitRepository;
    }

    public void addFruit(AddFruitRequest request) {
        fruitRepository.addFruit(request.getName(), request.getWarehousingDate(), request.getPrice());
    }

    public void updateFruit(UpdateFruitRequest request) {
        if (fruitRepository.isFruitNotExist(request.getId())) {
            throw new IllegalArgumentException("과일을 찾을 수 없습니다");
        }

        fruitRepository.updateFruit(request.getId());
    }

    public FruitSalesResponse findByName(String name) {
        List<Long> salesAmounts = fruitRepository.findByName(name);

        Long salesAmount = salesAmounts.get(0);
        Long notSaleAmount = salesAmounts.get(1);

        return new FruitSalesResponse(salesAmount, notSaleAmount);
    }
}
```

### Repository

```java

@Repository
public class FruitRepository {

    private final JdbcTemplate jdbcTemplate;

    public FruitRepository(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    @Override
    public void addFruit(String name, LocalDate warehousingDate, long price) {
        String sql = "INSERT INTO fruit (name, warehousing_date, price) VALUES (?, ?, ?)";
        jdbcTemplate.update(sql, name, warehousingDate, price);
    }

    @Override
    public List<Long> findByName(String name) {
        String sql = "SELECT SUM(price) FROM fruit WHERE name = ? GROUP BY is_sold";
        return jdbcTemplate.query(sql, (rs, rowNum) -> rs.getLong(1), name);
    }

    @Override
    public boolean isFruitNotExist(long id) {
        String readSql = "SELECT * FROM fruit WHERE id = ?";
        return jdbcTemplate.query(readSql, (rs, rowNum) -> 0, id).isEmpty();
    }

    @Override
    public void updateFruit(long id) {
        String sql = "UPDATE fruit SET is_sold = 1 WHERE id = ?";
        jdbcTemplate.update(sql, id);
    }
}
```

기존 코드보다 역할이 분명해진 점을 확인할 수 있다. 다시 정리하면 Controller, Service, Repository는 다음과 같은 역할을 가진다.

- Controller: HTTP와 관련된 기능
- Service: 트랜잭션에 대한 제어, 다양한 도메인을 필요로 하는 로직의 일부
- Repository: 저장소에서 도메인을 가져오는 기능

## 문제 2

- 강의를 참고하여 최소한으로 구성했다.

Repository를 나누기 위해 인터페이스(interface)를 생성하고 상속하여 구현하는 방식으로 진행했다.

```java
public interface FruitRepository {

    void addFruit(String name, LocalDate warehousingDate, long price);

    List<Long> findByName(String name);

    void updateFruit(long id);

    boolean isFruitNotExist(long id);
}
```

### @Primary

```java

@Primary
@Repository
public class FruitMySqlRepository implements FruitRepository {
}

@Repository
public class FruitMemoryRepository implements FruitRepository {
}
```

구현한 저장소에 `@Repository`를 사용하고 동작시키고 싶은 저장소에 `@Primary`를 사용한다.

- 여러 구현체를 가진 동일한 인터페이스를 사용할 때 어떤 빈을 주입할지 지정해야 한다.

- `@Primary` 또는 `@Qualifier`를 사용하지 않으면 에러가 발생한다.

### @Qualifier

정의

```java

@Repository
@Qualifier("mysql")
public class FruitMySqlRepository implements FruitRepository {
    // 구현
}

@Repository
@Qualifier("memory")
public class FruitMemoryRepository implements FruitRepository {
    // 구현
}
```

주입

```java

@Autowired
@Qualifier("mysql")
private FruitRepository mysqlRepository;

@Autowired
@Qualifier("memory")
private FruitRepository memoryRepository;
```

## 마치며

간단한 문제였지만 이외에도 다양한 시도를 해서 얻은 지식이 많았다. 추가로 고민했던 내용은 다음과 같다.

- 메모리 데이터베이스 데이터를 어떻게 미리 넣어둘 수 있을까?: `@EventListener`
- MemoryRepository를 제대로 구현해야 하는가?: 요구사항을 오버한다고 생각하여 최소한으로 구성했다.

리팩터링 전에 테스트 코드가 작성되어 있었다면 진행상황을 확인하며 더욱 재밌게 문제를 풀지 않았을까 하는 생각이 들었다. 테스트 코드도 얼른 배우고 리팩터링을 진행해야겠다.
