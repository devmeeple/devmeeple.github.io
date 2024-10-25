---
title: "Mock을 마주합니다. 그런데 Test Fixture를 곁들인"
description: ""
date: 2024-10-25 17:13:16
update: 2024-10-25 17:13:16
tags:
  - 스터디
  - 워밍업클럽
  - 인프런
series: 
---

![인프런 워밍업 클럽 스터디 2기 - 백엔드 클린 코드, 테스트 코드 <출처: 인프런>](../images/inflearn-warmup-club-study-2.png)

> *인프런 워밍업 클럽 2기, 18일차 미션을 '나만의 언어'로 정리한 글이다.

## 1. @Mock, @MockBean, @Spy, @SpyBean, @InjectMocks 차이는 무엇일까?

### 1.1 @Mock vs. @MockBean

`@Mock`은 Mockito에서 제공한다. 반면 `@MockBean`은 Spring에서 제공한다.

### 1.2 @Spy vs. @SpyBean

`@Spy`는 Mockito에서 제공한다. 반면 `@SpyBean`은 Spring에서 제공한다.

### 1.3 @InjectMocks

테스트 대상 객체(SUT, System Under Test)에 `@Mock`이 사용된 모의 객체 의존성을 편리하게 주입하기 위해 사용한다.
단위 테스트에 적합하고, 통합 테스트를 작성할 때는 `@Autowired`를 주로 사용한다.

### 1.4 결론

![의도된 바가 전해져야 돼요 <출처: 흑백요리사: 요리 계급 전쟁>](culinary-class-wars-intention.avif)

**테스트 코드를 작성할 때 '의도'를 전달할 수 있어야 한다.** 순수 단위 테스트가 필요하다면 `@Mock`, `@Spy`를 요구사항에 맞춰 사용한다.
반면 `Spring Context`가 필요한 통합 테스트라면 `@Bean 시리즈`를 사용해야 한다.

## 2. Test Fixture 구성하기

```java

@BeforeEach
void setUp() {
    ❓
}

@DisplayName("사용자가 댓글을 작성할 수 있다.")
@Test
void writeComment() {
    1 - 1. 사용자 생성에 필요한 내용 준비
    1 - 2. 사용자 생성
    1 - 3. 게시물 생성에 필요한 내용 준비
    1 - 4. 게시물 생성
    1 - 5. 댓글 생성에 필요한 내용 준비
    1 - 6. 댓글 생성

    // given
    ❓

    // when
    ❓

    // then
    검증
}

@DisplayName("사용자가 댓글을 수정할 수 있다.")
@Test
void updateComment() {
    2 - 1. 사용자 생성에 필요한 내용 준비
    2 - 2. 사용자 생성
    2 - 3. 게시물 생성에 필요한 내용 준비
    2 - 4. 게시물 생성
    2 - 5. 댓글 생성에 필요한 내용 준비
    2 - 6. 댓글 생성
    2 - 7. 댓글 수정

    // given
    ❓

    // when
    ❓

    // then
    검증
}

@DisplayName("자신이 작성한 댓글이 아니면 수정할 수 없다.")
@Test
void cannotUpdateCommentWhenUserIsNotWriter() {
    3 - 1. 사용자1 생성에 필요한 내용 준비
    3 - 2. 사용자1 생성
    3 - 3. 사용자2 생성에 필요한 내용 준비
    3 - 4. 사용자2 생성
    3 - 5. 사용자1의 게시물 생성에 필요한 내용 준비
    3 - 6. 사용자1의 게시물 생성
    3 - 7. 사용자1의 댓글 생성에 필요한 내용 준비
    3 - 8. 사용자1의 댓글 생성
    3 - 9. 사용자2가 사용자1의 댓글 수정 시도

    // given
    ❓

    // when
    ❓

    // then
    검증
}
```

주어진 예제는 다음과 같다.

## 마치며

![믿기 힘든 반전의 결과 속출 <출처: Show Me The Money 6>](show-me-the-money-6-fail.avif)

마지막 미션인 만큼 의심을 한 번 더 했다. 특히 2번 문제, Test Fixture 구성하기를 의심했다. '우빈 님께서 `setUp` 메서드에도
물음표를 사용하셨지만 함정이 아닐까?' 돌다리를 두드려 봤다. 하지만 거듭 생각해도 생각이 바뀌지 않았다.
미션, 과정 전부 끝났다. 배움이 많았다. 자세한 이야기는 '인프런 워밍업 클럽 2기 후기'로 알아보자.

**<참고 자료>**

- [박우빈 'Practical Testing: 실용적인 테스트 가이드'](https://inf.run/yoBRZ)
- [Baeldung 'Mockito.mock() vs @Mock vs @MockBean'](https://www.baeldung.com/java-spring-mockito-mock-mockbean)
- [Baeldung 'Difference Between @Spy and @SpyBean'](https://www.baeldung.com/spring-spy-vs-spybean)
- [Baeldung 'Using @Autowired and @InjectMocks in Spring Boot Tests'](https://www.baeldung.com/spring-test-autowired-injectmocks)
