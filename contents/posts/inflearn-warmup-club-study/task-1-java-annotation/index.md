---
title: "1. 자바 어노테이션"
description:
date: 2024-04-29 06:34:49
update: 2024-04-29 06:34:49
tags:
  - Java
series: "인프런 워밍업 클럽 - 스터디 BE 1기"
---

![인프런 워밍업 클럽 - 스터디 1기](../images/inflearn-warmup-club-study.png)

드디어 스터디가 시작됐다. 첫 번째 과제는 자바 어노테이션(Java Annotation)에 대해 알아보는 질문 & 답변 시간이다. 어노테이션의 어떤 점이 중요해서 첫 번째 과제로 선정됐을까?

```text 
💡 [질문] 

1. 어노테이션을 사용하는 이유(효과)는 무엇일까? 
2. 나만의 어노테이션을 어떻게 만들 수 있을까? 

``` 

질문에 답하기 이전에 어노테이션이 무엇인지 먼저 알아보자.

## 어노테이션이란?

어노테이션은 Java SE 5에 등장했다. 출시된 지 무려 20년을 앞둔 기능이다. (참고로 Generic, Enum도 이때 등장했다)

어노테이션이 도입되기 전에는 메타데이터(코드에 대한 부가 정보)를 자바코드에 직접 작성할 수 없었다. 메타데이터를 표현하기 위해서는 별도의 파일이나 외부 도구를 통해 관리했다. 예를 들어,
메서드가 상위 클래스의 메서드를 오버라이드하고 있다는 사실을 표현하려면 주석을 달거나 문서화해야 했다.

```java 
public class Ezreal extends Champion {
    // 오버라이드 된 메서드 
    public void attack() {
        // 상위 클래스의 메서드를 오버라이드 한다는 사실을 알려주는 방법이 없다. 
    }
} 
``` 

이런 식으로 `attack()`메서드는 오버라이드가 된 메서드임을 나타냈다. 어노테이션을 적극적으로 사용하는 현재, 다음과 같이 작성된 코드는 어딘가 부자연스럽다. 유지보수 시 주석이 누락되거나 잘못 작성되었다면
어땠을까?

```java 
public class Ezreal extends Champion {
    @Override
    public void attack() {
        // @Override 어노테이션으로 오버라이드 사실을 명시 
    }
} 
``` 

반면 어노테이션이 새롭게 도입되면서 메타데이터를 자바코드 내에 직접 포함할 수 있게 됐다. 이를 통해 코드의 가독성과 유지 보수성이 향상됐다.

현재 우리는 어노테이션을 흔하게 접할 수 있다. 예를 들어 자주 사용하는 라이브러리, 프레임워크에서 접할 수 있다.

- [Lombok 라이브러리](https://projectlombok.org/)

```java 

@Getter
@Setter
public class User {
    private String name;
    private String age;
} 
``` 

- [Spring 프레임워크](https://docs.spring.io/spring-framework/reference/index.html)

```java 

@Service
public class UserService {
    //... 
} 
``` 

- [JUnit 테스트 프레임워크](https://junit.org/junit5/)

```java 
public class UserTest {

    @Test
    public void testCreateUser() {
        // 테스트 코드 
    }
} 
``` 

이렇게 어노테이션은 다양한 라이브러리와 프레임워크에서 이미 활용되고 있다.

### 커스텀 어노테이션(나만의 어노테이션)

어노테이션을 만들려면 어떻게 해야 할까? `@interface` 문법을 사용하여 사용자 정의 어노테이션을 만들 수 있다.

```java 

@Target(ElementType.TYPE) // 클래스에만 적용 가능 
@Retention(RetentionPolicy.RUNTIME) // 런타임까지 유지 
public @interface Book {
    String title();

    String author();
} 
``` 

어노테이션에 포함될 요소와 데이터 유형을 지정하고, 메타데이터(@Retention, @Target 등)를 지정한다. 이렇게 어노테이션을 정의하고 사용할 수 있다.

### 주의점

어노테이션의 강력한 기능을 알아봤다. 하지만 과도하게 사용하면 오히려 역효과가 날 수 있다.

1. 가독성저하: 코드가 복잡해져 가독성이 떨어질 수 있다.
2. 의존성증가: 특정 어노테이션에 의존하게 되면 라이브러리, 프레임워크의 버전이 업그레이드 시 이슈가 발생할 수 있다.
3. 성능저하: 어노테이션 처리를 위해 리플렉션을 사용하는 경우, 성능 저하가 발생할 수 있다.

## 마치며

앞서 어노테이션에 대해 알아봤다. 이제 질문에 답할 시간이다.

개발자들은 흔히 좋은 코드, 나쁜 코드에 대해 이야기한다. 절대적인 정답은 없지만 나쁜 코드에 대해 이야기할 때 **같은 코드의 반복**을 이야기하곤 한다.
코드의 반복을 줄이는 여러 방법 중 어노테이션도 하나의 방법이다. 이는 코드의 가독성과 유지보수성을 향상한다. 또한 컴파일러나 개발 도구에 특정 정보를 제공하여 추가 기능을 활용할 수 있다. (리플렉션을 통한
메타데이터 접근)

> 물론 자바 본질에서 벗어날 수 있는 위기도 있다. 예를 들어 애노테이션(코드에 주석처럼 달아 특수한 의미를 부여하는 기술)의 범람이 대표적이다. 애노테이션은 코드를 적게 작성하고, 더 빠르게 앱을 개발할 수
> 있다는 점에서 장점이 있었다.
> 그러나 애노테이션은 한계가 있었다. 컴파일러에 의해 검증이 불가능하고 상속 확장 규칙의 표준이 없었다. 이해하기 어렵고 오해하기 쉬운 코드가 생산될 수 있으며, 테스트 및 커스터마이징이 어려웠다. 자바의 본질과
> 멀어졌다.
>
> 📝 기사 | 인터뷰 <[자바가 죽었다구요? 천만의 말씀](https://byline.network/2017/08/31-3/)> by 토비(이일민)

- 은빛 총알은 없다

> No Silver Bullet – Essence and Accident in Software Engineering
>
> 📝
> 논문 <[No Silver Bullet — Essence and Accident in Software Engineering](https://ko.wikipedia.org/wiki/%EC%9D%80%EB%B9%9B_%EC%B4%9D%EC%95%8C%EC%9D%80_%EC%97%86%EB%8B%A4)>
> by Fred Brooks

그렇다면 어노테이션은 모든 문제를 해결할 수 있을까? 그렇지 않다. 어노테이션 역시 장단점이 있으므로, 상황에 따라 적절하게 사용해야 한다. 프로젝트의 요구사항이 맞는지, 복잡성을 고려하여 사용여부를 결정해야 한다.
어노테이션은 강력한 도구지만 은빛 총알은 아니라는 점을 명심해야 한다.

추가로 나만의 커스텀 어노테이션을 직접 만들지 않아도 이미 대부분의 기능이 각 라이브러리, 프레임워크에서 제공 중이다. 따라서 검색과 공식문서를 통해 해결할 수 있는 방법이 없는지 먼저 확인하자.

### 함께 자라기

- [인프런 질문 & 답변 어노테이션 by 김영한님](https://www.inflearn.com/questions/91272/comment/78583)
- [Don't repeat yourself(DRY)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [Baeldung Creating a Custom Annotation in Java](https://www.baeldung.com/java-custom-annotation)
- [Oracle The Java Tutorials](https://docs.oracle.com/javase/tutorial/java/annotations/)
