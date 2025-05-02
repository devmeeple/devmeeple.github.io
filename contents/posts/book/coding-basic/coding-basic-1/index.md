---
title: "1장 효율적으로 언어 배우기"
description: ""
date: 2025-05-01 20:00:00
update: 2025-05-02 18:00:00
tags:
  - 독서
series: 코딩을 지탱하는 기술
---

> 이 글은 『코딩을 지탱하는 기술』을 읽고 생각과 지식을 덧붙여 정리했다. 책 내용과 100% 일치하지 않기 때문에 자세한 내용은 원문 참고를 권장한다.

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/3AoeaZs8dFemFJr3JdzOL0?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

어떻게 최적화하면 언어를 더욱 재밌게, 효과적으로 학습할 수 있을까? 학습법은 항상 고민하는 주제다. 새로운 언어를 배울 때 시작부터 중요한 점을 가려내기란 쉽지 않다. 효과적으로 언어를 배우는 방법 2가지를 제안한다.

### 1.1 비교를 통한 배움

> Java에서는 참거짓 값을 위한 형을 가지고 있어서 조건식에서도 그 형을 사용하지 않으면 안 된다. 0은 단순히 정수형을 의미하기 때문에 조건식에 0을 사용하게
> 되면 컴파일 에러가 발생한다.

```groovy
class NumberTruthyTest {

    @DisplayName("숫자 0을 조건식에 사용하면 falsy로 평가한다")
    @Test
    void shouldTreatZeroAsFalsyInCondition() {
        def number = 0

        def result = evaluateNumberTruthiness(number)

        assertEquals('0은 falsy', result)
    }

    @Test
    @DisplayName("0 이외의 숫자는 truthy로 평가한다")
    void shouldTreatNonZeroAsTruthyInCondition() {
        def number = 1

        def result = evaluateNumberTruthiness(number)

        // then
        assertEquals('0 이외의 숫자는 truthy', result)
    }

    private static String evaluateNumberTruthiness(def number) {
        if (number) {
            return '0 이외의 숫자는 truthy'
        } else {
            return '0은 falsy'
        }
    }
}
```

- Java의 조건식(Condition)은 `Boolean` 자료형을 사용해야 한다. 다른 자료형을 허용하지 않는다.
- 대부분의 정적 타입 기반 JVM 언어(Java, Kotlin, Scala 등)는 조건식에 `Boolean` 자료형만 허용한다. 하지만 [Groovy](https://groovy-lang.org/)처럼 동적 타입
  기반 언어는 `truthy/falsy` 개념을 지원한다.

## 1.2 역사를 통한 배움

### 언어 설계자의 의도를 이해하자

> 프로그래밍 언어도 사람이 만든 것이다. 언어 설계자는 어떤 문제를 해결하기 위해 그 언어를 만든 것일까? 그 언어가 어떤 흐름을 따라 만들어졌는지 알게 되면
> 그 기능이 왜 필요한지 납득할 수 있게 된다.

![James Gosling씨, 당신의 의도는 무엇인가요? <출처: JetBrains>](jetbrains-james-gosling.jpg)


- Java는 네트워크 장치, 임베디드 시스템 등 '다양한 환경에서 동작하는 언어'를 위해 개발했다.
- Java 문법은 C, C++의 영향을 받았다.
- Java는 처음에 Oak라고 불렸지만 Green이라는 이름을 거쳐 Java로 최종 변경됐다.

## 마치며

![간절함이 보내온 신호 우리의 시간은 이어져 있다 <출처: 시그널>](signal.jpg)

프로젝트 실습 외에 언어를 학습할 때 어떤 방식을 선택하면 좋을지 고민하다 선택했던 방법 2가지를 제안해서 놀라웠다. 두 가지 방법 모두 흥미롭지만 역사를 통해 배웠을 때 특히 재미를 느꼈다. 따분하게 느껴진다면 선배들의 간절함을 떠올려보자.

### 참고 자료

- [Wikipedia 'Java (programming language)'](https://en.wikipedia.org/wiki/Java_(programming_language))
- [Oracle 'Introduction to Java TM Technology'](https://www.oracle.com/java/technologies/introduction-to-java.html)